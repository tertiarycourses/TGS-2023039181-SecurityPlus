# Lab 26 — Endpoint Detection with osquery

You will install osquery, ask SQL questions of the live host, and schedule a query that detects a suspicious process.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `osquery`

---

## Step 1 — Install

```bash
export OSQUERY_KEY=1484120AC4E9F8A1A577AEEE97A80C63C9D8B80B
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys $OSQUERY_KEY 2>/dev/null
add-apt-repository -y 'deb [arch=amd64] https://pkg.osquery.io/deb deb main'
apt update && apt install -y osquery
osqueryi --version
```

---

## Step 2 — Interactive SQL queries

```bash
osqueryi --json "SELECT name, pid, uid FROM processes WHERE on_disk = 0;"  # in-memory only
osqueryi --json "SELECT name, version FROM deb_packages WHERE name LIKE 'openssh%';"
osqueryi --json "SELECT username, type FROM users WHERE shell != '/usr/sbin/nologin';"
osqueryi --json "SELECT * FROM listening_ports WHERE address = '0.0.0.0';"
```

Every system fact — process, package, port, user — is a SQL table. This is what makes osquery the open-source EDR primitive.

---

## Step 3 — Detect a "fileless" process

Simulate a process whose binary has been deleted:

```bash
cp /bin/sleep /tmp/.evil; /tmp/.evil 600 &
rm /tmp/.evil
osqueryi --json "SELECT name, pid, path FROM processes WHERE on_disk = 0;"
```

This is a classic indicator of malware that unlinks itself after launch.

---

## Step 4 — Detect new SUID binaries

```bash
osqueryi --json "SELECT path, mode FROM file WHERE path LIKE '/usr/bin/%' AND (mode LIKE '%4%') LIMIT 10;"
```

---

## Step 5 — Schedule the queries (osqueryd)

```bash
cat > /etc/osquery/osquery.conf <<'EOF'
{
  "options": { "logger_path": "/var/log/osquery", "schedule_splay_percent": 10 },
  "schedule": {
    "fileless_proc": { "query": "SELECT name, pid FROM processes WHERE on_disk = 0;", "interval": 60 },
    "new_listeners": { "query": "SELECT pid, port, address FROM listening_ports;", "interval": 60 },
    "users": { "query": "SELECT username, uid FROM users;", "interval": 300 }
  }
}
EOF
mkdir -p /var/log/osquery
systemctl enable --now osqueryd
sleep 70
ls /var/log/osquery
tail -3 /var/log/osquery/osqueryd.results.log
```

The results stream as JSON — feed them into Wazuh, ELK, or Splunk for centralised EDR/XDR.

---

## Step 6 — File integrity (FIM) with osquery

```bash
cat >> /etc/osquery/osquery.conf <<'EOF'
,
  "file_paths": { "etc": ["/etc/passwd", "/etc/shadow", "/etc/sudoers"] },
  "exclude_paths": { },
  "events": { "disable_subscribers": [] }
EOF
```

(Use `osqueryctl` to validate JSON before restart in production.)

---

## Free online tools

- **osquery docs** — https://osquery.readthedocs.io
- **Fleet (open source EDR console)** — https://fleetdm.com
- **Velociraptor** — https://docs.velociraptor.app
- **Sysmon for Linux** — https://github.com/Sysinternals/SysmonForLinux
- **Atomic Red Team** (test detections) — https://atomicredteam.io

---

## What you learned
- That EDR is fundamentally "ask SQL questions of the endpoint".
- The two highest-signal queries (`on_disk=0`, new listening ports).
- How osqueryd's JSON results plug straight into a SIEM.
