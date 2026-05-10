# Lab 18 — Data at Rest: LUKS Full-Disk Encryption

You will create an encrypted volume with LUKS2, mount it, rotate its passphrase, and add a keyfile — the standard "data at rest" control.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `cryptsetup`

---

## Step 1 — Install

```bash
apt update && apt install -y cryptsetup
```

---

## Step 2 — Create a 50 MB virtual disk file

```bash
dd if=/dev/zero of=vault.img bs=1M count=50
losetup -fP --show vault.img
LOOP=$(losetup -j vault.img | awk -F: '{print $1; exit}')
echo "Loop device: $LOOP"
```

---

## Step 3 — Format with LUKS2 (AES-XTS-512)

```bash
echo -n "Lab1234!" | cryptsetup luksFormat --type luks2 \
    --cipher aes-xts-plain64 --key-size 512 --hash sha256 \
    --pbkdf argon2id "$LOOP" -
cryptsetup luksDump "$LOOP" | head -25
```

`argon2id` is the modern key-derivation function — memory-hard against GPU cracking.

---

## Step 4 — Open, format, mount

```bash
echo -n "Lab1234!" | cryptsetup luksOpen "$LOOP" vault -
mkfs.ext4 -q /dev/mapper/vault
mkdir -p /mnt/vault
mount /dev/mapper/vault /mnt/vault
echo "secret data" > /mnt/vault/file.txt
ls -l /mnt/vault
```

---

## Step 5 — Confirm encryption

```bash
umount /mnt/vault
cryptsetup luksClose vault
strings vault.img | grep -i "secret data" || echo "not found in plaintext (good)"
```

The plaintext is unrecoverable from the raw image.

---

## Step 6 — Rotate the passphrase (key escrow workflow)

```bash
echo -n "Lab1234!" | cryptsetup luksOpen "$LOOP" vault -
echo -e "Lab1234!\nNewPass!9" | cryptsetup luksChangeKey "$LOOP"
cryptsetup luksClose vault
```

---

## Step 7 — Add a key-file slot (for unattended boot)

```bash
dd if=/dev/urandom of=/root/luks.key bs=1 count=64
chmod 400 /root/luks.key
echo -n "NewPass!9" | cryptsetup luksAddKey "$LOOP" /root/luks.key -
cryptsetup luksDump "$LOOP" | grep -E "Slot|Key Slot"
```

In production the key-file lives in a TPM-bound location or a KMS.

---

## Free online tools

- **VeraCrypt (cross-platform FDE)** — https://www.veracrypt.fr
- **BitLocker recovery key portal (Microsoft)** — https://account.microsoft.com/devices/recoverykey
- **AWS KMS (free tier)** — https://aws.amazon.com/kms/
- **HashiCorp Vault (open source)** — https://developer.hashicorp.com/vault
- **NIST SP 800-111 storage encryption** — https://csrc.nist.gov/publications/detail/sp/800-111/final

---

## What you learned
- The role of cipher (AES-XTS) vs. KDF (argon2id) in disk encryption.
- That LUKS supports up to 8 key slots — enabling rotation and escrow.
- Why a TPM/KMS-backed keyfile is the production answer to unattended unlock.
