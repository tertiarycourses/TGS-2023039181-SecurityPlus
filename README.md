# CompTIA Security+ SY0-701 Hands-On Labs

This repository provides a complete set of **36 step-by-step labs** aligned to the [CompTIA Security+ SY0-701 exam objectives](CompTIA-Security-Plus-SY0-701-Exam-Objectives.pdf).

These labs are the official hands-on companion for the **WSQ — CompTIA Certified Security+ Training** course (Course Code: **TGS-2023039181**) offered by **Tertiary Infotech Academy Pte Ltd**.

📘 **Register here:** https://www.tertiarycourses.com.sg/wsq-comptia-security-certification-prep.html

## Platform

All labs run on the free **Killercoda Ubuntu Playground** in your browser:

**https://killercoda.com/playgrounds/scenario/ubuntu**

No installs are required on your own machine. Every package is pulled with `apt` (or a single binary download) inside the throw-away VM. Reset the playground between labs that change firewall, PAM, or routing state.

## Curriculum

The 36 labs are organised across the five SY0-701 domains:

| Domain | Title | Labs | Weight |
|--------|-------|------|--------|
| 1.0 | General Security Concepts             | 5 | 12% |
| 2.0 | Threats, Vulnerabilities & Mitigations| 8 | 22% |
| 3.0 | Security Architecture                  | 7 | 18% |
| 4.0 | Security Operations                    | 10 | 28% |
| 5.0 | Security Program Management & Oversight| 6 | 20% |

Open [labs/README.md](labs/README.md) for the full lab index with links and software prerequisites.

## Tooling

Every tool used is **100% free** (open source, freeware, or free tier with no time limit). The complete inventory — grouped by category and lab number — is in [labs/tools.md](labs/tools.md). Highlights:

- **Crypto / PKI**: openssl, gnupg, cryptsetup, testssl.sh
- **Network defence**: iptables, nftables, ufw, wireguard, suricata, modsecurity
- **Identity**: PAM, sudo, fail2ban, google-authenticator
- **Detection**: osquery, aide, Wazuh SIEM
- **Vulnerability / pentest**: nmap, nikto, nuclei, trivy, lynis, metasploit, hydra, john, sqlmap
- **Forensics / IR**: yara, sleuthkit, volatility (external)
- **Compliance**: OpenSCAP + SCAP Security Guide
- **Awareness**: GoPhish + MailHog

Free **online** tools (CyberChef, FIRST CVSS calculator, VirusTotal, SSL Labs, crt.sh, MITRE ATT&CK, etc.) are referenced in every individual lab and consolidated in `labs/tools.md`.

## Suggested order

Work through Domain 1 → 2 → 3 → 4 → 5 in numeric order. Each lab is self-contained.

## Legal & ethical use

Labs that involve scanning, exploitation, password cracking, phishing simulation, or DoS techniques (Labs 7, 9, 11, 32, 33, 34, 36) must be performed **only** against:

- Systems you own (the Killercoda VM, your own containers).
- Targets explicitly listed in a signed authorisation / Rules of Engagement.
- Public CTF / training ranges (HackTheBox, TryHackMe, Vulnhub).

Unauthorised use against third-party systems is illegal in most jurisdictions, including the **Singapore Computer Misuse Act (Cap. 50A)**.

## Reference

- [CompTIA Security+ SY0-701 Exam Objectives (v5.0)](CompTIA-Security-Plus-SY0-701-Exam-Objectives.pdf)
- Companion course: [Tertiary Infotech CompTIA Network+ N10-009 Labs](https://github.com/tertiarycourses/TGS-2025054472-NetworkPlus)
