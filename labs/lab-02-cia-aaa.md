# Lab 2 — CIA Triad and AAA on Linux

You will implement each leg of the **CIA triad** (Confidentiality, Integrity, Availability) and demonstrate **AAA** (Authentication, Authorization, Accounting) using only built-in Linux tools.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free):**
- `coreutils` (pre-installed)
- `openssh-server` (pre-installed)
- `sudo` (pre-installed)

---

## Step 1 — Confidentiality with file permissions

```bash
useradd -m alice
useradd -m bob
echo "salary: 120000" > /home/alice/secret.txt
chown alice:alice /home/alice/secret.txt
chmod 600 /home/alice/secret.txt
sudo -u bob cat /home/alice/secret.txt 2>&1 || echo "DENIED — confidentiality enforced"
```

`chmod 600` means only the owner can read/write — the simplest implementation of confidentiality.

---

## Step 2 — Integrity with SHA-256

```bash
sha256sum /home/alice/secret.txt > /tmp/secret.sha256
cat /tmp/secret.sha256
```

Tamper with the file and re-check:

```bash
echo "tampered" >> /home/alice/secret.txt
sha256sum -c /tmp/secret.sha256 || echo "Integrity FAILED"
```

A failed checksum proves the integrity control caught the change.

---

## Step 3 — Availability with a service restart

```bash
systemctl status ssh --no-pager | head
systemctl restart ssh
ss -tlnp | grep :22
```

Availability means the service is **reachable when needed**. `ss -tlnp` confirms sshd is listening.

---

## Step 4 — Authentication: prove who you are

```bash
passwd alice <<EOF
Lab1234!
Lab1234!
EOF
su - alice -c 'whoami'
```

`su - alice` succeeds only when the correct password is provided.

---

## Step 5 — Authorization: what you can do

```bash
echo "alice ALL=(ALL) /usr/bin/cat /var/log/auth.log" >> /etc/sudoers
su - alice -c 'sudo cat /var/log/auth.log | head -3'
su - alice -c 'sudo cat /etc/shadow' 2>&1 | tail -1
```

Alice is *authenticated* but only *authorized* for one command.

---

## Step 6 — Accounting: log who did what

```bash
tail -20 /var/log/auth.log
```

Every `sudo` and `su` is logged with timestamp and user — the **accounting** leg of AAA.

---

## Free online tools

- **Hash Generator** — SHA-256 in the browser: https://alfredang.github.io/hashgenerator/
- **Cryptography Toolkit** — encode/decode/encrypt: https://alfredang.github.io/cryptography-toolkit/
- **OnlineHashCrack hash identifier** — https://www.onlinehashcrack.com/hash-identification.php
- **AAA explainer (Cloudflare)** — https://www.cloudflare.com/learning/access-management/what-is-aaa/

---

## What you learned
- How `chmod`, `sha256sum`, and `systemctl` map directly to C, I, and A.
- The difference between authentication (who) and authorization (what).
- Where Linux records the accounting trail required by AAA.
