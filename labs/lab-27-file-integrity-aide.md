# Lab 27 — File Integrity Monitoring with AIDE

You will baseline critical files with AIDE, modify one, and watch the diff report.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `aide`

---

## Step 1 — Install

```bash
apt update && apt install -y aide
aide --version
```

---

## Step 2 — Configure scope

```bash
cat > /etc/aide/aide.conf.d/99_lab <<'EOF'
/etc/passwd  NORMAL
/etc/shadow  NORMAL
/etc/sudoers NORMAL
/usr/bin     LSPP
/usr/sbin    LSPP
EOF
```

`NORMAL` checks size, perms, hashes. `LSPP` is the strict "Labelled Security Protection Profile" preset.

---

## Step 3 — Initialise the baseline

```bash
aideinit -y -f
mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
ls -lh /var/lib/aide/aide.db
```

The baseline is a SHA-256 fingerprint database. **Treat it like a key — back it up off-host.**

---

## Step 4 — First check (should report no changes)

```bash
aide --check | head -10
```

---

## Step 5 — Tamper and re-check

```bash
echo "# tampered $(date)" >> /etc/sudoers
useradd -m attacker
aide --check 2>&1 | head -25
```

AIDE reports the changed sudoers and the new shadow entry — exactly the signal a SOC needs.

---

## Step 6 — Roll the baseline forward (legitimate change)

After approved patches:

```bash
aide --update -B 'database_new=file:/var/lib/aide/aide.db.new'
mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

---

## Step 7 — Schedule a daily check

```bash
cat > /etc/cron.daily/aide-check <<'EOF'
#!/bin/sh
/usr/bin/aide --check | logger -t aide
EOF
chmod +x /etc/cron.daily/aide-check
```

Logs go to syslog → SIEM.

---

## Free online tools

- **AIDE docs** — https://aide.github.io
- **Tripwire Open Source** — https://github.com/Tripwire/tripwire-open-source
- **Samhain** — https://www.la-samhna.de/samhain
- **Wazuh FIM** — https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html

---

## What you learned
- A cryptographic baseline is the only reliable way to spot file tampering.
- The two operational mistakes: storing the DB on the host, never updating after patching.
- How to wire AIDE into syslog for SIEM correlation.
