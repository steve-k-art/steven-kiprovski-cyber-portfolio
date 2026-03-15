# Steven Kiprovski – Cybersecurity Portfolio

Welcome to my cybersecurity portfolio. This repository demonstrates hands-on security testing projects completed during my **Advanced Diploma of Cyber Security**, conducted entirely within isolated virtual lab environments.

---

## 👤 Author

**Steven Kiprovski**
Sydney, Australia
🔗 [github.com/steve-k-art](https://github.com/steve-k-art) linkedin.com/in/steven-kiprovski(https://www.linkedin.com/in/steven-kiprovski-b6b488387/)

---

## 📜 Certification

**Advanced Diploma of Cyber Security (ICT60220)**
Practical coursework covering penetration testing methodologies, network security, web application security, security infrastructure design, risk assessment, and GRC frameworks.

---

## 🧠 Skills Demonstrated

- Network Reconnaissance & Host Discovery
- Vulnerability Assessment & CVE Analysis
- Web Application Security Testing (OWASP Top 10)
- Penetration Testing & Exploit Implementation
- Virtualised Security Infrastructure Design & Implementation
- Red Team / Blue Team Operations
- SIEM Log Analysis & Intrusion Detection
- Security Risk Assessment & GRC Reporting
- Remediation Planning & Stakeholder Communication
- Tool Proficiency: `Nmap` `Nikto` `Hydra` `Metasploit` `Burp Suite` `OWASP ZAP` `Netcat` `Wfuzz` `Gobuster` `Splunk` `Kibana` `Security Onion` `OSSEC` `Snort` `Legion` `OpenVAS` `Wireshark`

---

## 📋 Project Index

| Project | Type | Key Tools |
|---------|------|-----------|
| [DataTrust – Vulnerability Assessment](#-vulnerability-assessment--datatrust) | Pentest / Vulnerability Assessment | Nmap, Nikto, Hydra, Metasploit, OpenVAS |
| [DataTrust – Cyber Infrastructure & Red/Blue Team](#-datatrust--cyber-infrastructure--redblue-team-exercise) | Infrastructure / Red-Blue Team | Security Onion, Splunk, Kibana, OSSEC, Legion |
| [OWASP Juice Shop – Web Application Testing](#-web-application-security-testing--owasp-juice-shop) | Web Application Security | Burp Suite, OWASP ZAP, Browser DevTools |
| [Network Reconnaissance Lab](#-network-reconnaissance-lab) | Reconnaissance & Enumeration | Nmap, ARP, nslookup, dig, traceroute |
| [Honeypot Penetration Testing](#-honeypot-penetration-testing) | Exploitation / Post-Exploitation | Gobuster, Wfuzz, Netcat, Burp Suite, Python |

---

## 📁 Projects

---

### 🛡️ Vulnerability Assessment – DataTrust

**[→ View Findings](projects/vulnerability-assessment-datatrust/README.md)**

A network and web service vulnerability assessment against a simulated enterprise environment (DataTrust). Performed full-scope scanning, enumeration, and exploitation across multiple services to identify and validate critical security weaknesses.

**Scope:** Internal network (10.5.1.x), Apache web server, OpenSSH 6.6.1p1, ProFTPD 1.3.5, phpMyAdmin, Jetty 8.1.7, MySQL

**Key Findings:**

| ID | Vulnerability | Severity | CVSS |
|----|--------------|----------|------|
| VA-01 | ProFTPD 1.3.5 Remote Code Execution | Critical | 9.8 |
| VA-02 | OpenSSH Authentication Bypass | High | 8.2 |
| VA-03 | Apache 2.4.7 Outdated / End-of-Life | High | 7.5 |
| VA-04 | phpMyAdmin Exposed — No Access Control | High | 7.2 |
| VA-05 | Missing HTTP Security Headers | Medium | 5.6 |

**Exploits Demonstrated:**
- OpenSSH brute force via Hydra (CVE-2016-6515)
- Apache Slowloris DoS via Metasploit (CVE-2007-6750)
- phpMyAdmin credential attack (CVE-2020-17530)

**Tools:** `Nmap` `Nikto` `OpenVAS` `Hydra` `Metasploit` `Burp Suite` `OWASP ZAP` `WHOIS`

---

### 🏗️ DataTrust – Cyber Infrastructure & Red/Blue Team Exercise

**[→ View Full Case Study](projects/datatrust-case-study/README.md)**

End-to-end virtualised enterprise security project covering infrastructure design, implementation, and adversarial testing. Built a 5-zone segmented network from scratch, then performed red team exploitation and blue team detection analysis against it.

**Scope:** 5-zone virtualised enterprise network — Internal, DMZ, External Testing, Security Zone, ISP simulation

**Infrastructure Built:**

| Device | IP | Role |
|--------|----|------|
| Security Onion | 192.168.0.1 / 10.30.0.1 | Centralised firewall, IDS, router |
| Splunk Server | 192.168.0.10 | Log collection & SIEM |
| Kali (Internal) | 192.168.0.100 | Defensive monitoring |
| Kali (External) | 192.168.1.100 | Offensive red team operations |
| Metasploitable 2 | 10.30.0.235 | Honeypot / primary target |
| Windows Server | 10.30.0.236 | DHCP, DNS, AD, Email |
| Web Server Farm | 10.30.0.237 | OWASP Juice Shop (port 3000) |

**Red Team — Exploits Executed:**
- vsftpd 2.3.4 backdoor → root shell (CVE-2011-2523)
- OpenSSH brute force → authenticated access (CVE-2016-6515)
- Apache Slowloris DoS → service outage (CVE-2007-6750)
- SMB port 445 brute force via Legion/Hydra → credential recovery
- XSS execution on web application via Burp Suite

**Blue Team — Detection & Monitoring:**
- 9,115 total log events captured across OSSEC, Syslog, Snort, and CRON
- 944 NIDS alerts generated; 803 classified (734 misc activity, 45 potentially bad traffic)
- Port scanning and HTTP exploit traffic detected via Kibana and Squert
- Gaps identified: MySQL attack and older CVE exploits not detected in real time

**Risk Assessment:** Initial and revised risk assessments produced with Australian legislative framework applied (Privacy Act 1988, Criminal Code Act 1995, Security of Critical Infrastructure Act 2018)

**Tools:** `Security Onion` `Splunk` `Kibana` `OSSEC` `Snort` `Squert` `Wireshark` `Metasploit` `Legion` `Hydra` `Nmap` `Nikto` `DIRB` `Burp Suite` `OWASP ZAP`

---

### 🍊 Web Application Security Testing – OWASP Juice Shop

**[→ View Findings](projects/web-application-testing-owasp/README.md)**

End-to-end web application security assessment against the OWASP Juice Shop — a deliberately vulnerable Node.js application. Testing was conducted across three difficulty levels covering the OWASP Top 10.

**Key Techniques Demonstrated:**
- SQL injection admin bypass
- DOM-based Cross-Site Scripting (XSS)
- CAPTCHA bypass
- Database schema extraction via UNION-based SQL injection
- Hidden endpoint discovery via automated spider scan
- API manipulation via Burp Suite Repeater
- Password brute force via Burp Suite Intruder

**Tools:** `Burp Suite` `OWASP ZAP` `Browser DevTools` `dirb`

---

### 🛰️ Network Reconnaissance Lab

**[→ View Findings](projects/network-reconnaissance-lab/README.md)**

Structured network reconnaissance engagement to identify active hosts, open ports, running services, and potential attack surfaces across a simulated enterprise network. Focused on passive and active enumeration techniques.

**Key Techniques Demonstrated:**
- Host discovery via ARP and ICMP
- Full port scan and service version detection with Nmap
- DNS enumeration via nslookup and dig
- Network topology mapping via traceroute
- Service banner grabbing and OS fingerprinting
- Attack surface documentation and reporting

**Tools:** `Nmap` `ARP` `nslookup` `dig` `traceroute` `Netcat`

---

### 🍯 Honeypot Penetration Testing

**[→ View Findings](projects/honeypot-penetration-testing/README.md)**

Penetration testing of two honeypot virtual machines (HP1VM and HP2VM). Achieved full remote code execution on both targets through different attack chains, demonstrating a range of web application and post-exploitation techniques.

**HP1VM Attack Chain:**
1. Nmap scan → identified Apache 2.4.38 on port 80
2. Wfuzz → discovered LFI vulnerability in `search1.php`
3. PHP filter exploit → extracted base64-encoded credentials
4. Reverse shell deployed → Netcat listener on port 1234
5. Remote code execution confirmed

**HP2VM Attack Chain:**
1. Gobuster → discovered hidden directories and `.htpasswd`
2. Nikto → identified file upload vulnerability
3. Webshell uploaded via vulnerable file upload function
4. Reverse shell deployed → full RCE confirmed

**Tools:** `Nmap` `Nikto` `Gobuster` `Wfuzz` `Netcat` `Burp Suite` `Python`

---

## 🖥️ Lab Environment

All testing was performed in an isolated virtual machine environment — no live or unauthorised systems were targeted at any point.

See **[lab-environment.md](lab-environment.md)** for full network topology, IP addressing, VM configurations, and zone architecture across all projects.

| Component | Details |
|-----------|---------|
| Attacker OS | Kali Linux 2024.3 |
| Virtualisation | VMware Workstation / VirtualBox |
| Network Type | Host-only / Internal (fully isolated) |
| Target Ranges | 10.5.1.x · 10.30.0.x · 192.168.0.x · 192.168.1.x · 192.168.112.x · 192.168.56.x |
| Targets | DataTrust server, DataTrust infrastructure (7 VMs), OWASP Juice Shop, HP1VM, HP2VM |

---

## 🛠️ Tools Reference

For a full breakdown of every tool used across this portfolio and how it was applied in each project, see **[tools-used.md](tools-used.md)**.

---

## ✅ Ethics & Scope

All activities in this portfolio were conducted:
- Exclusively within isolated virtual lab environments
- Against intentionally vulnerable or simulated systems only
- In accordance with the Advanced Diploma of Cyber Security program guidelines
- With no access to live, external, or unauthorised systems at any time
