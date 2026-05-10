# Lab 20 — Backup and Recovery with restic

You will configure encrypted, deduplicated backups, simulate ransomware, and perform a point-in-time restore.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `restic`

---

## Step 1 — Install

```bash
apt update && apt install -y restic
restic version
```

---

## Step 2 — Create a "production" data set and a backup repository

```bash
mkdir -p /data /backup
for i in $(seq 1 5); do echo "important record $i" > /data/rec$i.txt; done

export RESTIC_PASSWORD='Lab1234!'
restic -r /backup init
```

The repo is encrypted with the password — even if the backup disk is stolen the data is safe.

---

## Step 3 — Take the first snapshot

```bash
restic -r /backup backup /data
restic -r /backup snapshots
```

Note the snapshot ID — that is your **RPO checkpoint**.

---

## Step 4 — Modify data, take a second snapshot

```bash
echo "edit" >> /data/rec1.txt
echo "new record" > /data/rec6.txt
restic -r /backup backup /data
restic -r /backup snapshots
```

---

## Step 5 — Simulate ransomware

```bash
for f in /data/*.txt; do echo "ENCRYPTED_BY_RANSOMWARE" > "$f"; done
ls -l /data && cat /data/rec1.txt
```

---

## Step 6 — Restore from the previous snapshot

```bash
SNAP=$(restic -r /backup snapshots --json | python3 -c "import sys,json; print(json.load(sys.stdin)[-2]['id'])")
echo "Restoring snapshot $SNAP"
restic -r /backup restore $SNAP --target /restore
diff -r /restore/data /data
ls /restore/data
cat /restore/data/rec1.txt
```

You have just demonstrated **RTO** (time to recover) and **RPO** (data loss window).

---

## Step 7 — Apply 3-2-1 strategy

| Copy | Where                | What                |
|------|----------------------|---------------------|
| 1    | `/data` (production) | Live data           |
| 2    | `/backup` (local)    | Same machine snapshot |
| 3    | Off-site (S3, B2)    | `restic -r s3:...`  |

Initialise an off-site repo (example with the free Backblaze B2 tier):

```bash
# Replace with your B2 credentials, or use a local minio for testing
# export B2_ACCOUNT_ID=... B2_ACCOUNT_KEY=...
# restic -r b2:bucket:/path init
```

---

## Free online tools

- **Backblaze B2 (10 GB free)** — https://www.backblaze.com/b2
- **Wasabi** (S3-compatible cold storage) — https://wasabi.com
- **MinIO (self-hosted S3)** — https://min.io
- **rclone** (sync/encrypt) — https://rclone.org
- **NIST SP 800-34 Contingency Planning** — https://csrc.nist.gov/publications/detail/sp/800-34/rev-1/final

---

## What you learned
- restic combines encryption + deduplication + snapshots in one binary.
- Why the 3-2-1 rule survives ransomware, hardware failure, and regional outage.
- How to measure RTO and RPO from real restore timing.
