# TGS-2023039181 — CompTIA Security+ SY0-701 Hands-On Labs

> **Course:** WSQ — CompTIA Certified Security+ Training
> **Course Code:** TGS-2023039181
> **Register here:** https://www.tertiarycourses.com.sg/wsq-comptia-security-certification-prep.html

These are the official hands-on lab exercises for the WSQ CompTIA Certified Security+ Training course delivered by [**Tertiary Infotech Academy Pte Ltd**](https://www.tertiarycourses.com.sg/).

A complete set of **36 step-by-step labs** aligned to the [CompTIA Security+ SY0-701 exam objectives](CompTIA-Security-Plus-SY0-701-Exam-Objectives.pdf). Every lab runs on the free **Killercoda Ubuntu Playground** (https://killercoda.com/playgrounds/scenario/ubuntu) — no local install required.

---

## How to use

1. Open the Killercoda playground in your browser: https://killercoda.com/playgrounds/scenario/ubuntu
2. Pick a lab from the list below and follow the steps in order.
3. Reset the playground between labs that change firewall, PAM, or routing state.
4. See [labs/tools.md](labs/tools.md) for every free tool used (with install commands and download links).

---

## Lab catalogue

### Domain 1 — General Security Concepts (12%)
- [Lab 1 — Security Controls Categorization](labs/lab-01-security-controls.md)
- [Lab 2 — CIA Triad and AAA on Linux](labs/lab-02-cia-aaa.md)
- [Lab 3 — Hashing, Salting, and Digital Signatures](labs/lab-03-hashing-signatures.md)
- [Lab 4 — Symmetric vs. Asymmetric Encryption](labs/lab-04-symmetric-asymmetric.md)
- [Lab 5 — PKI: Build Your Own Certificate Authority](labs/lab-05-pki-ca.md)

### Domain 2 — Threats, Vulnerabilities & Mitigations (22%)
- [Lab 6 — Phishing Email Header Analysis (SPF/DKIM/DMARC)](labs/lab-06-phishing-email-analysis.md)
- [Lab 7 — Password Attacks: Spraying, Brute Force, Cracking](labs/lab-07-password-attacks.md)
- [Lab 8 — Malware Static Analysis (EICAR + YARA)](labs/lab-08-malware-static-analysis.md)
- [Lab 9 — SQL Injection (manual + sqlmap)](labs/lab-09-sql-injection.md)
- [Lab 10 — Cross-Site Scripting (XSS)](labs/lab-10-xss.md)
- [Lab 11 — DoS Simulation and Detection](labs/lab-11-dos-detection.md)
- [Lab 12 — Vulnerability Scanning with Nikto and Nuclei](labs/lab-12-vulnerability-scanning.md)
- [Lab 13 — Linux Hardening Baseline with Lynis](labs/lab-13-linux-hardening.md)

### Domain 3 — Security Architecture (18%)
- [Lab 14 — Network Segmentation with Linux Namespaces](labs/lab-14-network-segmentation.md)
- [Lab 15 — Stateful Firewall with UFW and nftables](labs/lab-15-firewall-ufw-nftables.md)
- [Lab 16 — Web Application Firewall with ModSecurity + OWASP CRS](labs/lab-16-waf-modsecurity.md)
- [Lab 17 — Site-to-Site VPN with WireGuard](labs/lab-17-vpn-wireguard.md)
- [Lab 18 — Data at Rest: LUKS Full-Disk Encryption](labs/lab-18-disk-encryption-luks.md)
- [Lab 19 — TLS Hardening and Cipher Audit](labs/lab-19-tls-hardening.md)
- [Lab 20 — Backup and Recovery with restic (3-2-1)](labs/lab-20-backup-recovery.md)

### Domain 4 — Security Operations (28%)
- [Lab 21 — SSH Hardening + Fail2ban](labs/lab-21-ssh-hardening-fail2ban.md)
- [Lab 22 — Identity & Access Management with PAM and sudo](labs/lab-22-iam-pam-sudo.md)
- [Lab 23 — Multi-Factor Authentication with TOTP](labs/lab-23-mfa-totp.md)
- [Lab 24 — SIEM Basics with Wazuh Manager](labs/lab-24-siem-elk-wazuh.md)
- [Lab 25 — Network IDS with Suricata](labs/lab-25-ids-suricata.md)
- [Lab 26 — Endpoint Detection with osquery](labs/lab-26-edr-osquery.md)
- [Lab 27 — File Integrity Monitoring with AIDE](labs/lab-27-file-integrity-aide.md)
- [Lab 28 — Vulnerability Management Pipeline with Trivy](labs/lab-28-vulnerability-management-trivy.md)
- [Lab 29 — Incident Response: Live-Triage and Forensics](labs/lab-29-incident-response-forensics.md)
- [Lab 30 — Automation & Orchestration (Mini-SOAR)](labs/lab-30-automation-soar.md)

### Domain 5 — Security Program Management & Oversight (20%)
- [Lab 31 — Risk Register, CVSS Scoring, and Quantitative Risk](labs/lab-31-risk-register-cvss.md)
- [Lab 32 — Passive Reconnaissance / OSINT](labs/lab-32-osint-recon.md)
- [Lab 33 — Active Reconnaissance with Nmap](labs/lab-33-active-recon-nmap.md)
- [Lab 34 — Penetration Testing with Metasploit](labs/lab-34-pentest-metasploit.md)
- [Lab 35 — Compliance Audit with OpenSCAP](labs/lab-35-compliance-openscap.md)
- [Lab 36 — Security Awareness: Phishing Simulation with GoPhish](labs/lab-36-phishing-awareness-gophish.md)

---

## Reference

- [labs/README.md](labs/README.md) — Lab index grouped by domain with software requirements
- [labs/tools.md](labs/tools.md) — Complete list of free tools (Killercoda + external)
- [CompTIA-Security-Plus-SY0-701-Exam-Objectives.pdf](CompTIA-Security-Plus-SY0-701-Exam-Objectives.pdf) — Official exam blueprint

---

## Free tools used

All tooling is **100% free** (open source, freeware, or free tier with no time limit). The bulk runs inside the disposable Killercoda VM via `apt` or a single binary download. A few labs also use free **online** services:

- **Cryptography Toolkit** — encrypt/decrypt in the browser (Labs 2, 4) — https://alfredang.github.io/cryptography-toolkit/
- **Hash Generator** — SHA/MD5/HMAC in the browser (Labs 2, 3) — https://alfredang.github.io/hashgenerator/
- **FIRST CVSS calculator** — score vulnerabilities (Lab 31)
- **VirusTotal / Hybrid Analysis / ANY.RUN** — multi-engine malware sandboxes (Lab 8)
- **SSL Labs / Mozilla Observatory** — TLS posture (Labs 12, 19)
- **crt.sh / Shodan / Censys** — passive recon (Lab 32)
- **MITRE ATT&CK / D3FEND / NIST** — frameworks and references (multiple labs)

Full tool list: [labs/tools.md](labs/tools.md).

---

## Legal & ethical use

Labs that involve scanning, exploitation, password cracking, phishing simulation, or DoS techniques (Labs 7, 9, 11, 32, 33, 34, 36) must be performed **only** against:

- Systems you own (the Killercoda VM, your own containers).
- Targets explicitly listed in a signed authorisation / Rules of Engagement.
- Public CTF / training ranges (HackTheBox, TryHackMe, Vulnhub).

Unauthorised use against third-party systems is illegal in most jurisdictions, including the **Singapore Computer Misuse Act (Cap. 50A)**.
