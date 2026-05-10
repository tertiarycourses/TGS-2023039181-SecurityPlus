# CompTIA Security+ SY0-701 — Lab Index

All labs run on the free **Killercoda Ubuntu Playground**:
**https://killercoda.com/playgrounds/scenario/ubuntu**

No installs are required on your own machine — every package is pulled with `apt` (or a single binary download) inside the throw-away VM. Reset the playground between labs that change firewall, routing, or PAM configuration.

---

## Domain 1 — General Security Concepts (12%)

| # | Lab | Free software needed |
|---|-----|----------------------|
| 1 | [Security Controls Categorization](lab-01-security-controls.md) | `iptables`, `auditd` (apt) |
| 2 | [CIA Triad and AAA on Linux](lab-02-cia-aaa.md) | `coreutils`, `sudo`, `openssh-server` (built-in) |
| 3 | [Hashing, Salting, Digital Signatures](lab-03-hashing-signatures.md) | `openssl` (built-in) |
| 4 | [Symmetric vs. Asymmetric Encryption](lab-04-symmetric-asymmetric.md) | `openssl`, `gnupg` (apt) |
| 5 | [PKI: Build Your Own CA](lab-05-pki-ca.md) | `openssl` (built-in) |

## Domain 2 — Threats, Vulnerabilities & Mitigations (22%)

| # | Lab | Free software needed |
|---|-----|----------------------|
| 6 | [Phishing Email Header Analysis (SPF/DKIM/DMARC)](lab-06-phishing-email-analysis.md) | `dnsutils`, `swaks` (apt) |
| 7 | [Password Attacks: Spraying, Brute Force, Cracking](lab-07-password-attacks.md) | `hydra`, `john` (apt) |
| 8 | [Malware Static Analysis (EICAR + YARA)](lab-08-malware-static-analysis.md) | `yara`, `binutils` (apt) |
| 9 | [SQL Injection (manual + sqlmap)](lab-09-sql-injection.md) | `sqlite3`, `php-cli`, `sqlmap` (apt) |
| 10 | [Cross-Site Scripting (XSS)](lab-10-xss.md) | `php-cli` (apt) |
| 11 | [DoS Simulation and Detection](lab-11-dos-detection.md) | `hping3`, `nginx` (apt) |
| 12 | [Vulnerability Scanning (Nikto + Nuclei)](lab-12-vulnerability-scanning.md) | `nikto`, `nuclei`, `apache2` (apt + binary) |
| 13 | [Linux Hardening Baseline with Lynis](lab-13-linux-hardening.md) | `lynis`, `unattended-upgrades` (apt) |

## Domain 3 — Security Architecture (18%)

| # | Lab | Free software needed |
|---|-----|----------------------|
| 14 | [Network Segmentation with Linux Namespaces](lab-14-network-segmentation.md) | `iproute2`, `iptables` (built-in) |
| 15 | [Stateful Firewall — UFW + nftables](lab-15-firewall-ufw-nftables.md) | `ufw`, `nftables`, `nginx` (apt) |
| 16 | [WAF with ModSecurity + OWASP CRS](lab-16-waf-modsecurity.md) | `nginx`, `libnginx-mod-http-modsecurity`, `modsecurity-crs` (apt) |
| 17 | [Site-to-Site VPN with WireGuard](lab-17-vpn-wireguard.md) | `wireguard`, `wireguard-tools` (apt) |
| 18 | [Data at Rest — LUKS Full-Disk Encryption](lab-18-disk-encryption-luks.md) | `cryptsetup` (apt) |
| 19 | [TLS Hardening and Cipher Audit](lab-19-tls-hardening.md) | `openssl`, `nginx`, `testssl.sh` (apt + git) |
| 20 | [Backup & Recovery with restic (3-2-1)](lab-20-backup-recovery.md) | `restic` (apt) |

## Domain 4 — Security Operations (28%)

| # | Lab | Free software needed |
|---|-----|----------------------|
| 21 | [SSH Hardening + Fail2ban](lab-21-ssh-hardening-fail2ban.md) | `fail2ban`, `openssh-server` (apt) |
| 22 | [IAM with PAM and sudo (RBAC)](lab-22-iam-pam-sudo.md) | `sudo`, `pam` (built-in) |
| 23 | [MFA with TOTP (Google Authenticator PAM)](lab-23-mfa-totp.md) | `libpam-google-authenticator`, `qrencode`, `oathtool` (apt) |
| 24 | [SIEM Basics with Wazuh](lab-24-siem-elk-wazuh.md) | Wazuh all-in-one installer (script) |
| 25 | [Network IDS with Suricata](lab-25-ids-suricata.md) | `suricata`, `jq` (apt) |
| 26 | [Endpoint Detection with osquery](lab-26-edr-osquery.md) | `osquery` (apt) |
| 27 | [File Integrity Monitoring with AIDE](lab-27-file-integrity-aide.md) | `aide` (apt) |
| 28 | [Vulnerability Management Pipeline (Trivy)](lab-28-vulnerability-management-trivy.md) | `trivy`, `docker.io` (apt) |
| 29 | [Incident Response: Live-Triage and Forensics](lab-29-incident-response-forensics.md) | built-in tools |
| 30 | [Automation & Orchestration (Mini-SOAR)](lab-30-automation-soar.md) | `inotify-tools`, `bash` (apt) |

## Domain 5 — Security Program Management & Oversight (20%)

| # | Lab | Free software needed |
|---|-----|----------------------|
| 31 | [Risk Register, CVSS, ALE](lab-31-risk-register-cvss.md) | `python3` + 🌐 FIRST CVSS calculator |
| 32 | [Passive Reconnaissance / OSINT](lab-32-osint-recon.md) | `theharvester`, `subfinder`, `whois` (apt + go) |
| 33 | [Active Reconnaissance with Nmap](lab-33-active-recon-nmap.md) | `nmap`, `nginx` (apt) |
| 34 | [Penetration Testing with Metasploit](lab-34-pentest-metasploit.md) | `metasploit-framework`, `docker.io` (apt) |
| 35 | [Compliance Audit with OpenSCAP](lab-35-compliance-openscap.md) | `libopenscap8`, `ssg-debian` (apt) |
| 36 | [Security Awareness — GoPhish Simulation](lab-36-phishing-awareness-gophish.md) | GoPhish binary, `mailhog` (docker) |

---

## Suggested order

Follow Domain 1 → 2 → 3 → 4 → 5 in numeric order. Each lab is self-contained. Reset the Killercoda playground between labs that change PAM, firewall, or routing state.

## Tools reference

See [tools.md](tools.md) for the complete free-software inventory used across all 36 labs, grouped by category and lab number.

## Legal & ethical reminder

Labs that involve scanning, exploitation, password cracking, phishing simulation, or DoS techniques (Labs 7, 9, 11, 32, 33, 34, 36) must be performed **only** against:

- Systems you own (the Killercoda VM, your own containers).
- Targets explicitly listed in a signed authorisation / Rules of Engagement.
- Public CTF / training ranges (HackTheBox, TryHackMe, Vulnhub).

Unauthorised use against third-party systems is illegal in most jurisdictions, including the **Singapore Computer Misuse Act (Cap. 50A)**.
