# Lab 15 — Stateful Firewall with UFW and nftables

You will compare two front-ends (UFW, nftables) over the same kernel netfilter engine, build an allow-list ruleset, and read its packet counters.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `ufw`
- `nftables`
- `nginx`

---

## Step 1 — Install

```bash
apt update && apt install -y ufw nftables nginx
systemctl start nginx
```

---

## Step 2 — UFW: an allow-list ruleset in three commands

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp comment 'SSH from anywhere'
ufw allow 80/tcp comment 'HTTP from anywhere'
ufw --force enable
ufw status numbered verbose
```

`default deny` is the cornerstone of any firewall. Anything not allowed is denied.

---

## Step 3 — Test the policy

```bash
curl -sI http://127.0.0.1 | head -1
nc -zv 127.0.0.1 23 2>&1
```

Port 80 succeeds, port 23 (Telnet) is denied.

---

## Step 4 — Inspect the underlying nftables ruleset

```bash
nft list ruleset | head -40
```

UFW translates its high-level commands into the same ruleset you would write directly.

---

## Step 5 — Write nftables directly

```bash
ufw --force disable
nft flush ruleset

cat > /etc/nftables.conf <<'EOF'
table inet filter {
  chain input {
    type filter hook input priority 0; policy drop;
    iif "lo" accept
    ct state established,related accept
    tcp dport {22, 80, 443} accept
    icmp type echo-request limit rate 5/second accept
    counter comment "dropped"
  }
  chain forward { type filter hook forward priority 0; policy drop; }
  chain output  { type filter hook output  priority 0; policy accept; }
}
EOF
systemctl enable --now nftables
nft list ruleset
```

---

## Step 6 — Watch counters under load

```bash
for i in $(seq 1 20); do curl -s http://127.0.0.1 >/dev/null; done
nft list chain inet filter input | grep counter
```

Counters give you packet/byte visibility per rule — the basis of firewall log analysis.

---

## Free online tools

- **pfSense Community Edition** — https://www.pfsense.org
- **OPNsense** — https://opnsense.org
- **firewalld docs** — https://firewalld.org
- **nftables wiki** — https://wiki.nftables.org
- **Shodan port-exposure lookup** — https://www.shodan.io

---

## What you learned
- UFW is a friendly skin over nftables/iptables; both produce identical kernel rules.
- The two unbreakable defaults: drop input, allow established+related.
- How counters expose what your firewall is actually doing.
