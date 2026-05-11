# Free Tools Reference — CompTIA Security+ SY0-701 Labs

Every tool listed here is **100% free** (open-source, freeware, or free tier with no time limit).

Two categories:

1. **Inside Killercoda** — installed in the disposable Ubuntu VM via `apt` or a single binary download. Nothing touches your own machine.
2. **External / Standalone** — downloaded onto your own PC/laptop, or used in a browser. Useful when you're offline, on a school PC, or want a GUI.

Killercoda playground (free, no signup): https://killercoda.com/playgrounds/scenario/ubuntu

---

## Section A — Tools installed inside the Killercoda Ubuntu VM

### A1. Cryptography & PKI
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `openssl` | pre-installed | Hash, encrypt, CA, TLS test | 3, 4, 5, 18, 19 |
| `gnupg` | `apt install gnupg` | OpenPGP encryption / signing | 4 |
| `cryptsetup` | `apt install cryptsetup` | LUKS full-disk encryption | 18 |

### A2. Identity, Access & Auth
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `sudo`, PAM | pre-installed | RBAC, time/lockout policies | 2, 22 |
| `libpam-google-authenticator` | `apt install libpam-google-authenticator` | TOTP MFA for SSH/login | 23 |
| `oathtool` | `apt install oathtool` | Generate TOTP from CLI | 23 |
| `qrencode` | `apt install qrencode` | Render TOTP QR codes | 23 |
| `openssh-server` | pre-installed | SSH + key auth | 2, 21, 23 |
| `fail2ban` | `apt install fail2ban` | Auto-ban brute-force IPs | 21 |

### A3. Network Security
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `iptables` / `nftables` | pre-installed / `apt install nftables` | Stateful firewall | 1, 11, 14, 15, 30 |
| `ufw` | `apt install ufw` | Friendly firewall front-end | 15 |
| `wireguard`, `wireguard-tools` | `apt install wireguard wireguard-tools` | Modern VPN | 17 |
| `iproute2` (`ip netns`) | pre-installed | Network namespaces / zoning | 14, 17 |
| `nginx` | `apt install nginx` | TLS / WAF target | 11, 15, 16, 19, 33 |
| `apache2` | `apt install apache2` | Web target for scanners | 12 |

### A4. Detection & Monitoring
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `auditd` | `apt install auditd` | Linux audit framework | 1 |
| `suricata` + `suricata-update` | `apt install suricata` | Open-source IDS/IPS | 25 |
| `osquery` | apt repo | EDR via SQL queries | 26 |
| `aide` | `apt install aide` | File integrity monitoring | 27 |
| `inotify-tools` | `apt install inotify-tools` | Filesystem event watcher | 30 |
| Wazuh | install script | Open-source SIEM (manager + agent) | 24 |

### A5. Vulnerability & Pentest
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `nmap` | `apt install nmap` | Port scanner / NSE | 33 |
| `nikto` | `apt install nikto` | Web vulnerability scanner | 12 |
| `nuclei` | binary release | Template-based vuln scanner | 12 |
| `trivy` | apt repo | Container / OS / secret scanner | 28 |
| `lynis` | `apt install lynis` | System hardening audit | 13 |
| `metasploit-framework` | apt repo | Exploitation framework | 34 |
| `hydra` | `apt install hydra` | Network login brute-force | 7 |
| `john` (the Ripper) | `apt install john` | Offline hash cracker | 7 |
| `sqlmap` | `apt install sqlmap` | Automated SQL injection | 9 |
| `hping3` | `apt install hping3` | Custom packet crafting / SYN flood | 11 |
| `theharvester` | `pip install theHarvester` | Email/host OSINT | 32 |
| `subfinder` | `go install ...` | Passive subdomain discovery | 32 |
| `whois`, `dnsutils` | `apt install whois dnsutils` | WHOIS / DNS lookups | 6, 32 |

### A6. Static Analysis & Forensics
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `yara` | `apt install yara` | Malware pattern matching | 8 |
| `binutils` (`strings`) | pre-installed | Extract printable strings | 8 |
| `file`, `coreutils` | pre-installed | File-type ID, hashing | 2, 8, 29 |
| `sleuthkit` (optional) | `apt install sleuthkit` | Disk forensics | 29 |

### A7. Compliance & Governance
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `libopenscap8` | `apt install libopenscap8` | SCAP scanner engine | 35 |
| `ssg-debian`, `ssg-debderived` | `apt install ssg-debian ssg-debderived` | CIS / STIG XCCDF content | 35 |
| `python3` | pre-installed | ALE/SLE math, JSON wrangling | 31 |

### A8. Backup & Resilience
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `restic` | `apt install restic` | Encrypted, deduplicated backup | 20 |

### A9. Mail / Phishing Lab
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `swaks` | `apt install swaks` | SMTP test client | 6 |
| MailHog | `docker run mailhog/mailhog` | Local SMTP sink (safe testing) | 36 |
| GoPhish | binary release | Phishing simulation platform | 36 |

### A10. Web Lab Targets
| Tool | Install | Purpose | Lab |
|------|---------|---------|-----|
| `php-cli`, `php-sqlite3` | `apt install php-cli php-sqlite3` | Vulnerable web apps | 9, 10 |
| `sqlite3` | `apt install sqlite3` | Lab database | 9 |
| `docker.io` | `apt install docker.io` | Run vulnerable / scanner containers | 28, 34, 36 |
| Metasploitable / DVWA images | `docker pull` | Authorised exploit targets | 34 |

---

## Section B — External / Standalone Free Tools (download or browser)

### B1. Cryptography & Encoding
| Tool | Type | Link |
|------|------|------|
| **Cryptography Toolkit** ⭐ used in many labs | Web | https://alfredang.github.io/cryptography-toolkit/ |
| **Hash Generator** ⭐ used in many labs | Web | https://alfredang.github.io/hashgenerator/ |
| OnlineHashCrack identifier | Web | https://www.onlinehashcrack.com/hash-identification.php |
| CrackStation | Web (look-up) | https://crackstation.net |
| Travis Tidwell RSA generator | Web | https://travistidwell.com/jsencrypt/demo/ |
| VeraCrypt | Win/Mac/Linux GUI | https://www.veracrypt.fr |

### B2. PKI / TLS
| Tool | Type | Link |
|------|------|------|
| Let's Encrypt | Free public CA | https://letsencrypt.org |
| SSL Labs Server Test | Web | https://www.ssllabs.com/ssltest |
| Mozilla SSL Config Generator | Web | https://ssl-config.mozilla.org |
| Hardenize | Web | https://www.hardenize.com |
| CipherSuite.info | Web | https://ciphersuite.info |
| crt.sh (Cert Transparency) | Web | https://crt.sh |
| testssl.sh | CLI | https://testssl.sh |

### B3. Email Anti-Spoofing (SPF / DKIM / DMARC)
| Tool | Type | Link |
|------|------|------|
| MXToolbox header analyzer | Web | https://mxtoolbox.com/EmailHeaders.aspx |
| Google Admin Toolbox Messageheader | Web | https://toolbox.googleapps.com/apps/messageheader/ |
| DMARC Analyzer | Web | https://www.dmarcanalyzer.com |
| PhishTool (free triage) | Web | https://www.phishtool.com |
| Have I Been Pwned | Web | https://haveibeenpwned.com |

### B4. Vulnerability Intel
| Tool | Type | Link |
|------|------|------|
| NVD / CVE search | Web | https://nvd.nist.gov |
| **FIRST CVSS calculator** ⭐ used in Lab 31 | Web | https://www.first.org/cvss/calculator/3.1 |
| FIRST CVSS v4 calculator | Web | https://www.first.org/cvss/calculator/4.0 |
| Ubuntu Security Tracker | Web | https://ubuntu.com/security/cves |
| GitHub Security Advisories | Web | https://github.com/advisories |
| OSV.dev open-source vuln DB | Web | https://osv.dev |
| CISA Known Exploited Vulns | Web | https://www.cisa.gov/known-exploited-vulnerabilities-catalog |
| Snyk free tier | Web | https://snyk.io |
| Greenbone OpenVAS Community | Self-hosted | https://www.greenbone.net |

### B5. Web Security / WAF
| Tool | Type | Link |
|------|------|------|
| OWASP CRS | Open ruleset | https://coreruleset.org |
| Cloudflare WAF (free tier) | Cloud | https://www.cloudflare.com |
| Mozilla Observatory | Web | https://observatory.mozilla.org |
| SecurityHeaders.com | Web | https://securityheaders.com |
| CSP Evaluator (Google) | Web | https://csp-evaluator.withgoogle.com |
| Wafw00f | CLI | https://github.com/EnableSecurity/wafw00f |
| OWASP Juice Shop (online) | Web | https://juice-shop.herokuapp.com |
| PortSwigger Web Security Academy | Free training | https://portswigger.net/web-security |

### B6. Malware Analysis (Online Sandboxes)
| Tool | Type | Link |
|------|------|------|
| VirusTotal | Web | https://www.virustotal.com |
| Hybrid Analysis | Web | https://www.hybrid-analysis.com |
| ANY.RUN community | Web | https://any.run |
| Joe Sandbox Cloud Basic | Web | https://www.joesandbox.com |
| MalwareBazaar (abuse.ch) | Web feed | https://bazaar.abuse.ch |

### B7. Recon / OSINT
| Tool | Type | Link |
|------|------|------|
| Shodan | Web | https://www.shodan.io |
| Censys | Web | https://search.censys.io |
| DNSDumpster | Web | https://dnsdumpster.com |
| SecurityTrails | Web | https://securitytrails.com |
| Hunter.io (free quota) | Web | https://hunter.io |
| OSINT Framework directory | Web | https://osintframework.com |
| Whoxy WHOIS | Web | https://www.whoxy.com |
| Hurricane Electric BGP | Web | https://bgp.he.net |

### B8. Identity / SSO / IdP
| Tool | Type | Link |
|------|------|------|
| Keycloak | Self-hosted | https://www.keycloak.org |
| FreeIPA | Self-hosted | https://www.freeipa.org |
| JumpCloud (free 10 users) | Cloud | https://jumpcloud.com |
| WebAuthn.io demo | Web | https://webauthn.io |
| Google / Microsoft Authenticator | Mobile | App stores |
| FreeOTP / Aegis | Mobile (FOSS) | https://freeotp.github.io / https://getaegis.app |
| YubiKey developer hub | Web | https://developers.yubico.com |

### B9. SIEM / SOC / SOAR
| Tool | Type | Link |
|------|------|------|
| Wazuh | Self-hosted | https://wazuh.com |
| Elastic stack (free) | Self-hosted | https://www.elastic.co |
| Splunk Free (500 MB/day) | Self-hosted | https://www.splunk.com |
| Graylog Open | Self-hosted | https://www.graylog.org |
| Security Onion | Self-hosted SOC distro | https://securityonionsolutions.com |
| TheHive (case mgmt) | Self-hosted | https://thehive-project.org |
| Shuffle SOAR | Self-hosted | https://shuffler.io |
| n8n automation | Self-hosted | https://n8n.io |
| MISP threat intel | Self-hosted | https://www.misp-project.org |
| Sigma rule repository | Open ruleset | https://github.com/SigmaHQ/sigma |

### B10. IDS / IPS / EDR
| Tool | Type | Link |
|------|------|------|
| Suricata | Open IDS/IPS | https://suricata.io |
| Snort 3 | Open IDS | https://www.snort.org |
| Zeek | Open NSM | https://zeek.org |
| osquery | Open EDR | https://osquery.io |
| Fleet (osquery console) | Open | https://fleetdm.com |
| Velociraptor | Open DFIR | https://docs.velociraptor.app |
| Sysmon for Linux | Open telemetry | https://github.com/Sysinternals/SysmonForLinux |
| Atomic Red Team | Detection tests | https://atomicredteam.io |

### B11. Forensics
| Tool | Type | Link |
|------|------|------|
| Autopsy / Sleuth Kit | GUI / CLI | https://www.sleuthkit.org |
| Volatility 3 | Memory forensics | https://github.com/volatilityfoundation/volatility3 |
| FTK Imager (free) | Win GUI | https://www.exterro.com/forensic-toolkit |
| Wireshark | All OSes | https://www.wireshark.org |
| Cryptography Toolkit | Web | https://alfredang.github.io/cryptography-toolkit/ |

### B12. Pentest / Red Team Practice Ranges (legal)
| Range | Type | Link |
|-------|------|------|
| HackTheBox | Cloud range | https://www.hackthebox.com |
| TryHackMe | Cloud range | https://tryhackme.com |
| Vulnhub | VM downloads | https://www.vulnhub.com |
| OWASP Juice Shop | Self-hosted | https://owasp.org/www-project-juice-shop |
| DVWA | Self-hosted | https://github.com/digininja/DVWA |
| PortSwigger Web Security Academy | Cloud training | https://portswigger.net/web-security |
| Metasploit Unleashed | Free training | https://www.offsec.com/metasploit-unleashed/ |

### B13. Phishing Simulation / Awareness
| Tool | Type | Link |
|------|------|------|
| GoPhish | Self-hosted | https://getgophish.com |
| King Phisher | Self-hosted | https://github.com/rsmusllp/king-phisher |
| PhishER (free tier) | Cloud | https://www.knowbe4.com/products/phisher |
| MailHog (SMTP sink) | Self-hosted | https://github.com/mailhog/MailHog |
| CISA phishing guidance | Web | https://www.cisa.gov/topics/cyber-threats-and-advisories/phishing |
| Google Phishing Quiz | Web | https://phishingquiz.withgoogle.com |

### B14. GRC / Risk / Compliance
| Tool | Type | Link |
|------|------|------|
| **FIRST CVSS calculator** | Web | https://www.first.org/cvss/calculator/3.1 |
| Eramba (open GRC) | Self-hosted | https://www.eramba.org |
| SimpleRisk | Self-hosted | https://www.simplerisk.com |
| InSpec by Chef | CLI | https://www.inspec.io |
| OpenSCAP / SCAP Security Guide | CLI | https://www.open-scap.org |
| CIS-CAT Lite | Win/Linux | https://www.cisecurity.org/cybersecurity-tools/cis-cat-lite |
| CIS Benchmarks (free PDFs) | Web | https://www.cisecurity.org/cis-benchmarks |
| DISA STIG library | Web | https://public.cyber.mil/stigs/ |
| NIST publications portal | Web | https://csrc.nist.gov/publications |
| MITRE ATT&CK | Web | https://attack.mitre.org |
| MITRE D3FEND | Web | https://d3fend.mitre.org |

### B15. Backup & Storage
| Tool | Type | Link |
|------|------|------|
| restic | CLI | https://restic.net |
| Backblaze B2 (10 GB free) | Cloud | https://www.backblaze.com/b2 |
| Wasabi (cold storage) | Cloud | https://wasabi.com |
| MinIO (self-hosted S3) | Self-hosted | https://min.io |
| rclone | CLI | https://rclone.org |

### B16. Browser sandboxes (Killercoda alternatives)
| Service | What you get | Link |
|---------|-------------|------|
| Killercoda Ubuntu Playground | Root Ubuntu shell | https://killercoda.com/playgrounds/scenario/ubuntu |
| Play with Docker | Linux VM | https://labs.play-with-docker.com |
| Replit | Linux shell + code | https://replit.com |
| GitHub Codespaces (free quota) | Cloud dev VM | https://github.com/features/codespaces |

---

## Lab → Primary Tool Quick Map

| Lab | Headline tool(s) |
|-----|------------------|
| 1  | iptables, auditd |
| 2  | chmod, sha256sum, sudo |
| 3  | openssl (sha256, dgst, passwd) |
| 4  | openssl, gpg |
| 5  | openssl ca / x509 |
| 6  | dig, swaks |
| 7  | hydra, john |
| 8  | strings, sha256sum, yara, VirusTotal |
| 9  | sqlmap, php, sqlite3 |
| 10 | php, curl, CSP |
| 11 | hping3, iptables limit, syncookies |
| 12 | nikto, nuclei, securityheaders.com |
| 13 | lynis, sysctl |
| 14 | ip netns, iptables FORWARD |
| 15 | ufw, nftables |
| 16 | ModSecurity, OWASP CRS |
| 17 | wireguard |
| 18 | cryptsetup luks2 |
| 19 | testssl.sh, openssl s_client |
| 20 | restic |
| 21 | sshd_config, fail2ban |
| 22 | sudoers, pam_time, pam_faillock |
| 23 | google-authenticator, oathtool |
| 24 | Wazuh manager |
| 25 | Suricata, ET Open, eve.json |
| 26 | osquery, osqueryd |
| 27 | aide |
| 28 | trivy |
| 29 | ps, ss, sha256sum, NIST IR phases |
| 30 | bash + iptables + tickets |
| 31 | Python ALE, FIRST CVSS calculator |
| 32 | whois, subfinder, theHarvester, crt.sh |
| 33 | nmap (-sS, -sV, NSE) |
| 34 | metasploit-framework, docker |
| 35 | OpenSCAP, ssg-debian profile |
| 36 | GoPhish, MailHog |

---

All tools above are free of charge. The Killercoda VM is also free and disposable, so you can run every lab without spending or installing anything on your own machine — except a couple of optional GUI tools in Section B.
