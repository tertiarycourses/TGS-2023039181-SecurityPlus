# Lab 4 — Symmetric vs. Asymmetric Encryption

You will encrypt the same file with AES-256 (symmetric) and with RSA + GPG (asymmetric) and compare the trade-offs.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `openssl` (pre-installed)
- `gnupg`

---

## Step 1 — Install GPG

```bash
apt update && apt install -y gnupg
```

---

## Step 2 — Symmetric encryption with AES-256

```bash
echo "top secret message" > msg.txt
openssl enc -aes-256-cbc -pbkdf2 -salt -in msg.txt -out msg.aes -pass pass:Lab1234!
xxd msg.aes | head
openssl enc -d -aes-256-cbc -pbkdf2 -in msg.aes -pass pass:Lab1234!
```

One key encrypts and decrypts. Fast, but how do you share `Lab1234!` with the other party?

---

## Step 3 — Generate an asymmetric key pair with GPG

```bash
gpg --batch --pinentry-mode loopback --passphrase '' \
    --quick-generate-key 'Alice <alice@lab.local>' rsa2048 default 1y
gpg --list-keys
gpg --armor --export alice@lab.local > alice.pub
```

`alice.pub` can be shared publicly. The matching private key never leaves the keyring.

---

## Step 4 — Encrypt with the public key, decrypt with the private key

```bash
gpg --yes --trust-model always -r alice@lab.local -e -o msg.gpg msg.txt
gpg --pinentry-mode loopback --passphrase '' -d msg.gpg
```

Anyone with `alice.pub` can encrypt **to** Alice; only Alice can read it. This is how PGP solves the key-distribution problem of Step 2.

---

## Step 5 — Hybrid encryption (the real-world pattern)

TLS, S/MIME, and PGP all use **asymmetric to wrap a symmetric key**, then the symmetric key encrypts the bulk data. Verify with:

```bash
gpg --list-packets msg.gpg | head -20
```

You will see a `pubkey enc packet` (RSA-wrapped session key) followed by an `encrypted data packet` (AES bulk data).

---

## Free online tools

- **CyberChef AES + RSA** — https://gchq.github.io/CyberChef/
- **PGPTool web** — https://pgptool.org
- **Keybase** (free PGP identity) — https://keybase.io
- **SSL/TLS cipher reference** — https://ciphersuite.info

---

## What you learned
- Symmetric is fast but suffers a key-distribution problem.
- Asymmetric solves distribution but is slow for bulk data.
- Real systems combine both (hybrid) — exactly what the GPG packet dump shows.
