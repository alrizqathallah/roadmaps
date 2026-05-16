# 🛡️ Cybersecurity Learning Roadmap
### From Beginner to Advanced — A Structured, Industry-Aligned Path

> **How to use this roadmap:** Progress sequentially through each phase. Complete all exercises and mini-projects before moving to the next phase. Mega-projects cap each major stage. Estimated total time: 18–24 months of consistent study (10–15 hrs/week).

---

## Table of Contents

1. [Phase 0 — Foundations](#phase-0--foundations-weeks-1-6)
2. [Phase 1 — Core Security Concepts](#phase-1--core-security-concepts-weeks-7-14)
3. [Phase 2 — Offensive Security (Red Team)](#phase-2--offensive-security-red-team-weeks-15-26)
4. [Phase 3 — Defensive Security (Blue Team)](#phase-3--defensive-security-blue-team-weeks-27-38)
5. [Phase 4 — Specialization Tracks](#phase-4--specialization-tracks-weeks-39-52)
6. [Phase 5 — Advanced & Professional](#phase-5--advanced--professional-weeks-53-72)
7. [Resources & Certifications](#resources--certifications)
8. [Lab Setup Guide](#lab-setup-guide)

---

## Phase 0 — Foundations (Weeks 1–6)

> **Goal:** Build the bedrock knowledge that everything else depends on. No security without solid fundamentals.

### 0.1 Networking Fundamentals

**Topics:**
- OSI & TCP/IP models — understand each layer's role
- IP addressing, subnetting, CIDR notation
- Core protocols: DNS, DHCP, HTTP/S, FTP, SSH, SMTP, ARP
- Packet structure and flow analysis
- Firewalls, NAT, VPNs at a conceptual level
- Wireshark basics: capturing and reading traffic

**Learning Materials:**
- *Professor Messer's CompTIA Network+* (free on YouTube)
- *Computer Networking: A Top-Down Approach* — Kurose & Ross (Ch. 1–4)
- TryHackMe: "Pre-Security" learning path (free)
- Cisco Packet Tracer (free simulator)

**Exercises:**
1. Subnet a /24 network into 8 equal subnets by hand — verify with an online calculator
2. Use Wireshark to capture your own HTTP traffic; identify source IP, destination, and payload
3. Run `nslookup`, `ping`, `traceroute` on 5 different domains and document the results
4. Draw the OSI model from memory and map each protocol you've learned to a layer

**Mini-Project — Home Network Audit:**
Document your home network: map all devices, their IPs, open ports (use `nmap`), and the protocols they expose. Write a one-page security assessment of what you find.

---

### 0.2 Operating Systems & Linux

**Topics:**
- Linux file system hierarchy and permissions (`chmod`, `chown`)
- Command-line fluency: navigation, text processing (`grep`, `awk`, `sed`), piping
- Process management, cron jobs, services (`systemctl`)
- Windows fundamentals: registry, Active Directory basics, PowerShell intro
- Virtualization: setting up VMs with VirtualBox/VMware
- Bash scripting basics

**Learning Materials:**
- *The Linux Command Line* — William Shotts (free online at linuxcommand.org)
- OverTheWire: Bandit wargame (levels 0–20)
- Microsoft Learn: Windows Server fundamentals (free)

**Exercises:**
1. Complete OverTheWire Bandit levels 0–15
2. Write a bash script that monitors a directory for new files and logs their name, size, and timestamp
3. Set up a Kali Linux VM and a Windows Server VM that can communicate on an internal network
4. Practice file permission scenarios: create files accessible only to specific users/groups

**Mini-Project — Automated System Health Monitor:**
Write a bash script that checks CPU, memory, disk usage, and running services every 5 minutes, appends results to a log file, and sends an alert (email or desktop notification) if any threshold is exceeded.

---

### 0.3 Programming for Security

**Topics:**
- Python basics: data types, loops, functions, file I/O, error handling
- Working with libraries: `requests`, `socket`, `subprocess`, `os`
- Reading and understanding code in other languages (Bash, PowerShell, basic C)
- Regular expressions for pattern matching
- Version control with Git

**Learning Materials:**
- *Automate the Boring Stuff with Python* — Al Sweigart (free online)
- HackerRank Python track (beginner/intermediate)
- *Black Hat Python* — Ch. 1–3 (preview of what's ahead)

**Exercises:**
1. Write a Python port scanner that accepts an IP and range, checks open ports, and prints results
2. Build a script that parses a web server access log and reports the top 10 IPs by request count
3. Create a password strength checker that evaluates length, character diversity, and common patterns
4. Write a script to rename 100 files in a directory following a naming convention

**Mini-Project — Network Reconnaissance Tool:**
Build a Python CLI tool that accepts a target IP or hostname and performs: ping check, port scan (top 20 ports), banner grabbing on open ports, and reverse DNS lookup. Output results to a structured report.

---

### ✅ Phase 0 Mega-Project — Personal Security Lab

Set up a complete virtual lab environment consisting of:
- Kali Linux (attacker machine)
- Windows Server 2019/2022 (target with Active Directory)
- Ubuntu Server (web/file server target)
- pfSense (virtual firewall/router)
- Metasploitable 2 or DVWA (intentionally vulnerable targets)

Document the setup with a network diagram, IP allocation table, and a "lab journal" explaining why each machine exists. This lab will be used throughout the entire roadmap.

---

## Phase 1 — Core Security Concepts (Weeks 7–14)

> **Goal:** Develop security thinking — confidentiality, integrity, availability — and understand how attacks and defenses relate.

### 1.1 Security Fundamentals & Frameworks

**Topics:**
- CIA Triad, AAA model (Authentication, Authorization, Accounting)
- Risk management: threat, vulnerability, likelihood, impact
- Security controls: preventive, detective, corrective
- Common frameworks: NIST CSF, ISO 27001, CIS Controls
- Compliance overview: GDPR, HIPAA, PCI-DSS (concepts, not deep-dive)
- Security policies and their purpose

**Learning Materials:**
- *CompTIA Security+ Study Guide* — Mike Chapple (Ch. 1–5)
- NIST Cybersecurity Framework (free PDF from nist.gov)
- (ISC)² Cybersecurity Certification entry-level modules (free)

**Exercises:**
1. Perform a simple risk assessment on a hypothetical small business (5 assets, identify threats, rate risk)
2. Map 10 real-world breaches (from HaveIBeenPwned news or Verizon DBIR) to CIA Triad failures
3. Write a 1-page Acceptable Use Policy for a fictional 50-person company
4. Compare NIST CSF and CIS Controls — create a table of how they overlap and differ

**Mini-Project — Risk Register:**
For a fictional e-commerce startup, build a complete risk register with 15+ risks, rated by likelihood and impact, with mitigation strategies assigned to each. Present it as a professional spreadsheet.

---

### 1.2 Cryptography Fundamentals

**Topics:**
- Symmetric encryption: AES, DES, key management
- Asymmetric encryption: RSA, ECC, public/private key pairs
- Hashing: MD5, SHA-1, SHA-256, bcrypt — and why they differ
- PKI, certificates, certificate authorities, TLS handshake
- Common attacks: brute force, rainbow tables, birthday attacks
- Practical tools: `openssl`, GPG

**Learning Materials:**
- *Serious Cryptography* — Jean-Philippe Aumasson (Ch. 1–6)
- Khan Academy: Cryptography course (free)
- Cryptohack.org — hands-on crypto challenges

**Exercises:**
1. Use `openssl` to generate a self-signed certificate, inspect it, and verify its chain
2. Crack MD5 hashes from CrackStation using a wordlist — document which failed and why
3. Implement Caesar cipher and ROT13 in Python; then implement AES-256 encryption using `cryptography` library
4. Complete 10 beginner challenges on Cryptohack

**Mini-Project — Secure File Vault:**
Build a Python CLI application that encrypts and decrypts files using AES-256, protects the key with a password-derived key (PBKDF2), and stores encrypted metadata. Include integrity verification using HMAC.

---

### 1.3 Web Technologies & Application Security

**Topics:**
- How the web works: HTTP methods, status codes, cookies, sessions, headers
- HTML, CSS, JavaScript at a read-level (no need to be a developer)
- Web application architecture: client, server, database, APIs
- OWASP Top 10 — conceptual understanding of each vulnerability
- Browser developer tools for security analysis
- Burp Suite Community Edition basics

**Learning Materials:**
- MDN Web Docs — HTTP overview (free)
- OWASP Top 10 official documentation (free at owasp.org)
- PortSwigger Web Security Academy (free — world-class resource)
- DVWA (Damn Vulnerable Web Application) in your lab

**Exercises:**
1. Intercept and modify a request in Burp Suite (use DVWA)
2. Identify and exploit each OWASP Top 10 vulnerability in DVWA at "Low" security level — document findings
3. Manually test a web app for missing security headers using browser dev tools and curl
4. Complete PortSwigger's "SQL Injection" lab series (beginner tier)

**Mini-Project — Web Vulnerability Scanner (Basic):**
Write a Python tool that crawls a target URL, checks for common misconfigurations (missing security headers, exposed admin panels, directory listing), and generates an HTML report.

---

### ✅ Phase 1 Mega-Project — Security Assessment Report

Perform a structured security assessment of DVWA (or a similar CTF target) covering:
- Information gathering and reconnaissance
- Vulnerability identification across web, network, and OS layers
- Risk rating for each finding (using CVSS scoring)
- Remediation recommendations

Deliver a professional-grade penetration test report (minimum 10 pages) following industry templates (Offensive Security or SANS report formats).

---

## Phase 2 — Offensive Security (Red Team) (Weeks 15–26)

> **Goal:** Learn to think and act like an attacker. Ethical hacking skills make you a dramatically better defender.

> ⚠️ **Ethics & Legality:** Only perform these techniques on systems you own or have explicit written permission to test. Always operate within the law.

### 2.1 Reconnaissance & OSINT

**Topics:**
- Passive vs. active reconnaissance
- OSINT techniques: Google dorking, Shodan, Maltego, theHarvester
- DNS enumeration, WHOIS, certificate transparency logs
- Social engineering reconnaissance
- Email and username enumeration
- OSINT framework overview

**Learning Materials:**
- *Open Source Intelligence Techniques* — Michael Bazzell (Ch. 1–8)
- osintframework.com — interactive tool map
- TryHackMe: "OSINT" room

**Exercises:**
1. Perform passive OSINT on a target company (use your own employer or a public company with permission) — find exposed emails, subdomains, and technology stack
2. Use `theHarvester` and `recon-ng` to enumerate a domain
3. Perform Google dorking to find exposed files (use only publicly indexed content on your own domain or lab)
4. Build an OSINT profile on a fictional persona you create

**Mini-Project — Target Dossier:**
Choose a bug bounty program target (from HackerOne or Bugcrowd in-scope assets) and perform full passive reconnaissance. Deliver a dossier including: org structure, tech stack, subdomains, employee emails, and potential attack surface — without touching any systems.

---

### 2.2 Scanning & Enumeration

**Topics:**
- Nmap: host discovery, port scanning, service detection, OS fingerprinting, scripting engine (NSE)
- Service enumeration: SMB, FTP, SSH, HTTP, RDP
- Vulnerability scanning with OpenVAS / Nessus Essentials
- Web enumeration: directory/file brute-forcing (Gobuster, ffuf)
- Subdomain enumeration: Amass, Subfinder
- Banner grabbing and version detection

**Learning Materials:**
- *Nmap Network Scanning* — Gordon Lyon (free online at nmap.org)
- TryHackMe: "Nmap" room
- HackTheBox Starting Point machines

**Exercises:**
1. Scan your lab network with Nmap using at least 5 different scan types — compare results
2. Use Nmap NSE scripts to enumerate SMB shares and detect vulnerabilities on Metasploitable
3. Run Gobuster against DVWA and document all discovered paths
4. Configure and run OpenVAS against your lab's vulnerable VMs — review the report

**Mini-Project — Automated Recon Pipeline:**
Build a bash/Python script that chains tools (Amass → Nmap → Gobuster → Nikto) for a given target domain, captures all output, deduplicates results, and generates a unified markdown recon report.

---

### 2.3 Exploitation Fundamentals

**Topics:**
- Metasploit Framework: architecture, modules, payloads, sessions
- Exploiting known CVEs (EternalBlue, MS17-010, etc.) in lab environments
- Manual exploitation vs. automated tools — when to use each
- Payload types: reverse shells, bind shells, Meterpreter
- Post-exploitation basics: whoami, network discovery, file exfiltration
- Covering tracks (for understanding — not for malicious use)

**Learning Materials:**
- *Metasploit: The Penetration Tester's Guide* — Kennedy et al. (Ch. 1–8)
- TryHackMe: "Metasploit" room
- VulnHub machines: Mr. Robot, Basic Pentesting 1 & 2

**Exercises:**
1. Exploit MS17-010 on a vulnerable Windows VM using Metasploit — achieve SYSTEM shell
2. Exploit a vulnerable FTP service on Metasploitable manually (without Metasploit)
3. Write a Python reverse shell from scratch and catch it with netcat
4. Perform post-exploitation on a compromised Linux machine: find credentials, escalate to root

**Mini-Project — Full Compromise Chain:**
Starting from zero, compromise a VulnHub machine end-to-end: reconnaissance → scanning → exploitation → post-exploitation → privilege escalation → capture the flag. Write a full technical walkthrough documenting every step, tool, and command used.

---

### 2.4 Web Application Penetration Testing

**Topics:**
- SQL Injection: manual detection, `sqlmap`, blind SQLi, out-of-band
- Cross-Site Scripting (XSS): reflected, stored, DOM-based
- IDOR, SSRF, XXE, File Inclusion (LFI/RFI)
- Authentication attacks: credential stuffing, session fixation, JWT abuse
- API security testing: REST, GraphQL vulnerabilities
- Business logic flaws

**Learning Materials:**
- PortSwigger Web Security Academy — complete all apprentice + practitioner labs
- *The Web Application Hacker's Handbook* — Stuttard & Pinto (Ch. 9–14)
- HackTheBox: Web challenges (easy/medium)

**Exercises:**
1. Complete all 15 PortSwigger SQL Injection labs
2. Complete all PortSwigger XSS labs (apprentice level)
3. Find and exploit an IDOR vulnerability in a vulnerable app — document impact and remediation
4. Crack a JWT token, forge a new one with admin privileges, and demonstrate the attack

**Mini-Project — Bug Bounty Report:**
Participate in a real bug bounty program (HackerOne/Bugcrowd — beginner-friendly programs like HackerOne's own H1 program). Find and report a valid vulnerability, even if low severity. Alternatively, write a complete simulated report for a vulnerability you found in a lab environment, formatted to industry standard.

---

### ✅ Phase 2 Mega-Project — Full Penetration Test

Conduct an end-to-end, simulated penetration test against a complex lab environment (set up 3–4 interconnected VMs or use a platform like HackTheBox Pro Labs "Offshore" or TryHackMe "Throwback"):

Deliverables:
- **Scoping document** — rules of engagement, objectives, timeline
- **Executive summary** — non-technical overview of findings and risk
- **Technical report** — detailed findings with evidence, CVSS scores, and reproduction steps
- **Remediation plan** — prioritized list of fixes
- **Lessons learned** — what worked, what didn't, what you'd do differently

This should mirror a real-world deliverable to a client. Aim for 20+ pages.

---

## Phase 3 — Defensive Security (Blue Team) (Weeks 27–38)

> **Goal:** Build, monitor, and defend systems. Understand attacker TTPs and how to detect and respond to them.

### 3.1 Security Operations & Monitoring

**Topics:**
- Security Operations Center (SOC) structure and analyst tiers
- SIEM concepts: log aggregation, correlation, alerting
- Setting up and using Splunk Free or ELK Stack (Elasticsearch, Logstash, Kibana)
- Log types: Windows Event Logs, Syslog, firewall logs, web logs
- Alert triage and investigation workflow
- MITRE ATT&CK framework — understanding TTPs

**Learning Materials:**
- Splunk Free Training: Splunk Fundamentals 1 (free)
- TryHackMe: "SOC Level 1" learning path
- MITRE ATT&CK documentation (attack.mitre.org — free)
- *The Practice of Network Security Monitoring* — Richard Bejtlich

**Exercises:**
1. Install ELK Stack in your lab; ingest Windows Event Logs from your Windows VM
2. Create 5 detection rules in your SIEM for common attack patterns (failed logins, large data transfers, new admin accounts)
3. Map a real-world attack scenario (e.g., ransomware kill chain) to MITRE ATT&CK techniques
4. Investigate a simulated alert: trace an event from SIEM alert → log source → host investigation

**Mini-Project — SOC Dashboard:**
Build a Kibana (or Splunk) dashboard for a fictional organization that visualizes: top alert types, geographic login anomalies, failed authentication trends, and privileged account activity over time.

---

### 3.2 Threat Intelligence & Hunting

**Topics:**
- Threat intelligence lifecycle: collection, processing, analysis, dissemination
- Indicator types: IoCs (IPs, hashes, domains), IoAs, TTPs
- Open-source threat intel: VirusTotal, AlienVault OTX, MISP, Shodan
- Threat hunting concepts: hypothesis-driven hunting
- Yara rules for malware detection
- STIX/TAXII standards

**Learning Materials:**
- SANS Cyber Threat Intelligence Summit talks (free on YouTube)
- OpenCTI documentation and tutorials
- TryHackMe: "Cyber Threat Intelligence" room

**Exercises:**
1. Enrich 10 IoCs from a public threat report using VirusTotal, Shodan, and OTX
2. Write 3 Yara rules that would detect variants of a known malware family (use any.run samples)
3. Perform a threat hunt in your SIEM for lateral movement indicators — document hypothesis, data sources, and findings
4. Ingest a threat feed into MISP and correlate it against your lab's logs

**Mini-Project — Threat Intelligence Report:**
Monitor a threat actor group (APT28, Lazarus, etc.) for one week using open sources. Write a professional threat intelligence report including: actor profile, recent campaigns, TTPs mapped to MITRE ATT&CK, and defensive recommendations relevant to a target industry.

---

### 3.3 Incident Response & Digital Forensics

**Topics:**
- IR lifecycle: Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned (PICERL)
- Memory forensics: Volatility framework
- Disk forensics: Autopsy, FTK Imager
- Network forensics: PCAP analysis with Wireshark, Zeek, NetworkMiner
- Log analysis for incident reconstruction
- Malware triage: static and dynamic analysis basics
- Chain of custody and legal considerations

**Learning Materials:**
- *The Art of Memory Forensics* — Ligh et al. (Ch. 1–5)
- SANS FOR500 / FOR508 free materials and cheat sheets
- TryHackMe: "Digital Forensics and Incident Response" path

**Exercises:**
1. Analyze a memory dump with Volatility — identify running processes, network connections, and injected code
2. Perform disk forensics on a provided image (from forensicscontest.com) — recover deleted files and timeline activity
3. Analyze a PCAP file to reconstruct an attack sequence — what happened, when, who was involved?
4. Conduct a simulated IR exercise: a "ransomware infection" in your lab — contain, investigate, and document

**Mini-Project — Incident Response Playbook:**
Create a complete IR playbook for a ransomware incident, including: detection criteria, stakeholder notification matrix, containment checklist, forensic evidence collection procedures, communication templates, and recovery steps. Format it as an operational runbook.

---

### 3.4 Hardening & Secure Architecture

**Topics:**
- CIS Benchmarks for Windows, Linux, and cloud services
- Defense in depth and zero trust architecture principles
- Network segmentation, DMZ design, firewall rule management
- Endpoint Detection and Response (EDR) concepts
- Identity and Access Management: MFA, PAM, least privilege
- Patch management and vulnerability management programs
- Secure configuration management

**Learning Materials:**
- CIS Benchmarks (free download at cisecurity.org)
- NIST SP 800-53 overview
- Microsoft Defender documentation (hardening guides)

**Exercises:**
1. Apply CIS Level 1 benchmark hardening to your Ubuntu VM — document every change and its purpose
2. Design a secure network architecture for a 100-person company: draw the diagram with all security controls labeled
3. Implement and test firewall rules on pfSense in your lab — block C2 traffic while allowing legitimate traffic
4. Write a PowerShell script to audit Windows systems against 20 CIS benchmark items

**Mini-Project — Hardened Server Deployment:**
Deploy a hardened web server (Apache/Nginx on Ubuntu) from scratch: apply CIS benchmarks, configure WAF rules (ModSecurity), enforce TLS 1.2+, implement fail2ban, centralize logs to your SIEM, and document the full hardening checklist with evidence of each control.

---

### ✅ Phase 3 Mega-Project — Purple Team Exercise

Conduct a full purple team exercise in your lab:

**Red actions (attacker):**
- Spear phishing simulation (using GoPhish against your own lab user)
- Lateral movement via pass-the-hash
- Data exfiltration via DNS tunneling

**Blue actions (defender):**
- Detect each red action in your SIEM
- Write detection rules for each TTP
- Contain and eradicate the simulated threat
- Produce a post-incident timeline

**Deliverable:** A purple team report documenting each attack technique (mapped to MITRE ATT&CK), whether it was detected, detection gap analysis, and tuning recommendations for the SIEM.

---

## Phase 4 — Specialization Tracks (Weeks 39–52)

> **Goal:** Go deep in one or two domains aligned with your career goals and market demand.

Choose at least ONE primary track and optionally a secondary track.

---

### Track A — Cloud Security

**Industry Demand:** Very High | **Avg. Salary Premium:** 20–35%

**Topics:**
- Shared responsibility model (AWS, Azure, GCP)
- IAM misconfigurations and privilege escalation in cloud
- Cloud-native attacks: metadata service abuse, S3 bucket exposure, Lambda exploitation
- CSPM tools: Prowler, ScoutSuite, Checkov
- Cloud security frameworks: CSA CCM, AWS Well-Architected
- Container and Kubernetes security basics

**Key Resources:**
- *Hacking the Cloud* — hackingthe.cloud (free)
- CloudGoat — Rhino Security Labs (intentionally vulnerable AWS)
- ACloudGuru / AWS Security Specialty prep
- flaws.cloud and flaws2.cloud challenges (free)

**Exercises & Projects:**
1. Complete all flaws.cloud challenges — document each misconfiguration
2. Set up a vulnerable S3 bucket in a personal AWS free-tier account; discover and remediate it
3. Perform IAM privilege escalation in CloudGoat lab environment
4. Write Terraform code for a secure, CIS-compliant AWS landing zone

**Track Mega-Project:** Deploy a 3-tier web application on AWS with full security controls: WAF, CloudTrail, GuardDuty, Security Hub, encrypted S3, tight IAM roles, VPC with private subnets. Write a security architecture document and simulate an attack against it.

---

### Track B — Application Security (AppSec)

**Industry Demand:** Very High | **Avg. Salary Premium:** 15–30%

**Topics:**
- Secure Software Development Lifecycle (SSDLC)
- Threat modeling: STRIDE, DREAD, attack trees
- SAST, DAST, SCA tools and CI/CD integration
- Code review for security: Python, JavaScript, Java vulnerabilities
- Supply chain security and dependency management
- Secure API design and OAuth 2.0 / OpenID Connect deep dive

**Key Resources:**
- OWASP SAMM (Software Assurance Maturity Model)
- *The Tangled Web* — Michal Zalewski
- Semgrep documentation and rules
- Snyk Learn (free interactive secure coding)

**Exercises & Projects:**
1. Perform a threat model on a simple e-commerce checkout flow using STRIDE
2. Integrate Semgrep into a GitHub Actions pipeline — write 3 custom rules
3. Conduct a manual code review of a vulnerable Python Flask app (find 5+ vulnerabilities)
4. Design a secure OAuth 2.0 implementation diagram for a mobile app

**Track Mega-Project:** Build a security review program for a fictional development team: create a threat modeling template, integrate 3 SAST/SCA tools into a CI/CD pipeline, write a secure coding standard document, and produce a security review of a sample codebase with findings and fixes.

---

### Track C — Red Team / Adversary Simulation

**Industry Demand:** High | **Avg. Salary Premium:** 15–25%

**Topics:**
- Advanced exploitation: buffer overflows, ROP chains (intro level)
- Active Directory attacks: Kerberoasting, AS-REP Roasting, DCSync, Golden/Silver Tickets
- C2 frameworks: Cobalt Strike concepts, Sliver, Havoc
- Evasion techniques: AV bypass, AMSI bypass, obfuscation
- Physical security and social engineering methodology
- Red team reporting and debrief

**Key Resources:**
- *Penetration Testing* — Georgia Weidman
- HackTheBox Pro Labs: RastaLabs, Offshore
- SpecterOps blog posts and training materials
- TryHackMe: "Advanced exploitation" paths

**Exercises & Projects:**
1. Perform Kerberoasting in your AD lab — crack service account hashes
2. Execute a full AD attack chain: initial access → lateral movement → domain compromise
3. Write a custom C2 implant in Python (for lab use only) that beacons to a server
4. Practice bypassing Windows Defender using publicly known techniques in an isolated lab

**Track Mega-Project:** Conduct a simulated adversary campaign emulating a real APT group (choose one from MITRE ATT&CK groups). Follow their documented TTPs, attempt to achieve their documented objectives in your lab, and write a red team report including executive narrative, technical findings, and detection recommendations.

---

### Track D — Governance, Risk & Compliance (GRC)

**Industry Demand:** High | **Avg. Salary Premium:** 10–20%

**Topics:**
- ISO 27001 implementation and audit process
- NIST RMF (Risk Management Framework) in depth
- PCI-DSS compliance requirements and gap assessments
- Third-party risk management (TPRM)
- Security awareness program design
- Audit evidence collection and control testing

**Key Resources:**
- ISO 27001 standard overview (free summaries on iso.org)
- NIST SP 800-37 (RMF guide — free)
- ISACA CISA study materials

**Exercises & Projects:**
1. Conduct a gap assessment of a fictional company against ISO 27001 Annex A controls
2. Write a complete Business Continuity Plan (BCP) for a 200-person financial firm
3. Design a security awareness training curriculum for non-technical employees
4. Create a vendor risk questionnaire and scoring matrix for 3rd party SaaS vendors

**Track Mega-Project:** Develop a complete Information Security Management System (ISMS) for a fictional mid-size company: scope definition, risk register, policy library (10+ policies), control implementation plan, KPI dashboard, and audit evidence templates — packaged as a professional governance deliverable.

---

## Phase 5 — Advanced & Professional (Weeks 53–72)

> **Goal:** Achieve professional-grade expertise, contribute to the community, and establish a track record.

### 5.1 Advanced Topics by Domain

**Malware Analysis & Reverse Engineering:**
- Static analysis: PE structure, strings, imports, `pestudio`, `Detect-It-Easy`
- Dynamic analysis: sandboxes (`any.run`, Cuckoo), API monitoring, ProcMon
- Disassembly: Ghidra (free) and IDA Free for basic RE
- Writing Yara and Sigma rules from malware samples

**Exercises:**
1. Analyze a real malware sample from MalwareBazaar (in an isolated VM) — document capabilities, IoCs, and MITRE ATT&CK mapping
2. Unpack a simple UPX-packed binary manually
3. Reverse engineer a simple CTF crackme challenge using Ghidra

**Zero Trust Architecture Design:**
- Identity-centric security model
- Micro-segmentation strategies
- Continuous verification and device trust
- Designing ZTA for hybrid environments

**Advanced Threat Hunting:**
- Hunting with Splunk/ELK at scale
- Sigma rule development and sharing
- Building detection-as-code pipelines
- Behavioral analytics and ML-assisted detection

---

### 5.2 Capture The Flag (CTF) Practice

CTFs are the best way to develop creative problem-solving under constraint.

**Recommended Platforms:**
- PicoCTF — excellent for all levels (free)
- CTFtime.org — calendar of live competitions
- HackTheBox — machines and challenges
- pwn.college — binary exploitation focus

**Strategy:**
- Compete consistently (aim for 2–4 CTFs per year)
- Focus on your weak categories first
- Always write post-competition writeups — this builds your portfolio
- Collaborate with teams via CTFtime team formation

**Milestone:** Achieve a ranking in the top 30% of participants in at least one public CTF competition.

---

### 5.3 Portfolio & Career Development

**Building Your Portfolio:**
- GitHub profile: publish tools, scripts, CTF writeups (no malicious code)
- Personal blog or Medium: document your learning journey and walkthroughs
- LinkedIn: professional profile with certifications, projects, and endorsements
- Bugcrowd/HackerOne: public Hall of Fame entries if possible

**Networking:**
- Attend DEF CON, Black Hat, BSides events (many have free/cheap options)
- Engage in communities: r/netsec, SANS Internet Storm Center, local security meetups
- Contribute to open-source security tools
- Mentor beginners — teaching accelerates your own learning

**Contributing Back:**
- Write and share Sigma/Yara rules to community repositories
- Report vulnerabilities through responsible disclosure
- Speak at a local BSides or university security club

---

### ✅ Phase 5 Mega-Project — Capstone Research Project

Choose a topic at the frontier of cybersecurity and produce an original research contribution:

**Examples:**
- Develop a novel detection technique for a specific evasion method
- Build and open-source a security tool that fills a gap you've identified
- Conduct original research on a vulnerability class and write a full technical paper
- Design and test a new security architecture pattern for a specific environment

**Deliverables:**
- Technical paper (2,000–5,000 words) — suitable for submission to a BSides or academic conference
- Working proof-of-concept code or tool (published on GitHub)
- Conference-style presentation slides
- A recorded demo or live presentation to a technical audience

---

## Resources & Certifications

### Certification Roadmap by Phase

| Phase | Certification | Provider | Cost | Value |
|-------|--------------|----------|------|-------|
| 0–1 | CompTIA A+ / Network+ | CompTIA | $$$  | Entry credential |
| 1 | CompTIA Security+ | CompTIA | $$$ | Industry baseline — widely required |
| 2 | eJPT (eLearnSecurity) | INE | $ | Practical offensive intro |
| 2 | CEH | EC-Council | $$$$ | Recognition in certain sectors |
| 2–3 | CompTIA PenTest+ | CompTIA | $$$ | Practical pentesting |
| 3 | CompTIA CySA+ | CompTIA | $$$ | Blue team baseline |
| 3–4 | Blue Team Labs certifications | BTLO | $ | Affordable hands-on |
| 4A | AWS Security Specialty | AWS | $$$ | Cloud security gold standard |
| 4B | CSSLP | (ISC)² | $$$$ | AppSec professional |
| 4C | OSCP (OffSec) | OffSec | $$$$ | Red team gold standard |
| 4D | CISM / CISA | ISACA | $$$$ | GRC leadership |
| 5 | CISSP | (ISC)² | $$$$ | Senior security leadership |

> **$ = <$200 | $$ = $200–500 | $$$ = $500–1000 | $$$$ = $1000+**

### Essential Free Resources

**Platforms:**
- TryHackMe.com — gamified, beginner-friendly
- HackTheBox.eu — more realistic, intermediate+
- PicoCTF — Carnegie Mellon CTF platform
- PortSwigger Web Security Academy — best free web security training
- SANS Cyber Aces — free fundamentals course

**Reading:**
- Krebs on Security (krebsonsecurity.com) — daily industry news
- The Hacker News (thehackernews.com) — threat intel and news
- Schneier on Security (schneier.com) — security thinking and policy
- SANS Reading Room — free research papers on every topic

**Practice:**
- VulnHub — free downloadable vulnerable VMs
- MalwareBazaar — real malware samples (for analysis, in isolated VMs)
- PCAP samples — wireshark.org sample captures
- Forensics challenges — forensicscontest.com

---

## Lab Setup Guide

### Minimum Hardware Requirements
- CPU: Intel Core i5/AMD Ryzen 5 or better (VT-x/AMD-V enabled)
- RAM: 16 GB (32 GB strongly recommended for Phase 3+)
- Storage: 500 GB free (SSD preferred)
- Network: Wired connection for lab work

### Essential Software (All Free)
- **Hypervisor:** VirtualBox (free) or VMware Workstation Player (free)
- **Attacker OS:** Kali Linux 2024.x — kali.org
- **Monitoring:** Elastic Stack (ELK) — elastic.co
- **Traffic Analysis:** Wireshark, Zeek
- **Web Testing:** Burp Suite Community, OWASP ZAP
- **Exploitation:** Metasploit Framework (included in Kali)
- **Forensics:** Autopsy, Volatility 3

### Recommended VM Inventory

| VM | OS | Role | RAM |
|----|-----|------|-----|
| Kali Linux | Debian-based | Attacker workstation | 4 GB |
| Windows Server 2022 | Windows | AD target | 4 GB |
| Ubuntu Server 22.04 | Linux | Web/file server target | 2 GB |
| Metasploitable 2 | Linux | Vulnerable target | 1 GB |
| pfSense | BSD | Firewall/router | 1 GB |
| ELK Stack | Ubuntu | SIEM | 4–8 GB |

### Network Topology
```
[Internet] → [pfSense Firewall]
                     │
           ┌─────────┴─────────┐
      [DMZ Network]       [Internal Network]
      192.168.10.0/24     192.168.20.0/24
      - Ubuntu Web         - Windows Server (AD)
      - DVWA               - Workstations
                           │
                    [Attacker Network]
                    192.168.30.0/24
                    - Kali Linux
                    - ELK Stack
```

---

## Progress Tracking

### Skill Assessment Checkpoints

Use this checklist to validate readiness before advancing:

**Before Phase 1:** Can you subnet a network, analyze a PCAP, and write a Python port scanner?

**Before Phase 2:** Can you explain all OWASP Top 10 vulnerabilities, perform a risk assessment, and use Burp Suite to intercept requests?

**Before Phase 3:** Have you successfully exploited a machine end-to-end and written a pentest report?

**Before Phase 4:** Can you detect an attack in your SIEM, analyze a memory dump, and respond to a simulated incident?

**Before Phase 5:** Have you completed at least one specialization track and participated in a CTF?

---

*Last updated: 2025 | Always verify tool legality and ethical guidelines before use*
*This roadmap aligns with: NIST NICE Framework, CISA Workforce Development Guidelines, and industry job posting analysis*