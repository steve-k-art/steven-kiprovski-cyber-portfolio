# Steven Kiprovski — Cyber Security Portfolio

![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=flat&logo=kalilinux&logoColor=white)
![Metasploit](https://img.shields.io/badge/Metasploit-2596CD?style=flat&logo=metasploit&logoColor=white)
![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=flat&logo=burpsuite&logoColor=white)
![Splunk](https://img.shields.io/badge/Splunk-000000?style=flat&logo=splunk&logoColor=white)
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat&logo=wireshark&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-004170?style=flat&logoColor=white)

**Penetration Tester · SOC Analyst · Threat Analyst**
**Security Engineer · GRC Analyst**
📍 Sydney, Australia

---

## 🎓 Qualification

**ICT60220 — Advanced Diploma of Cyber Security**
Practical coursework covering penetration testing, network security, web application security, infrastructure design, red/blue team operations, risk assessment, and GRC frameworks.

---

## 📋 Projects

| Project | Type | Key Tools |
|---------|------|-----------|
| [Vulnerability Assessment – DataTrust](#️-vulnerability-assessment--datatrust) | Pentest / VA | Nmap · Nikto · Hydra · Metasploit · OpenVAS |
| [Web Application Testing – OWASP Juice Shop](#-web-application-security-testing--owasp-juice-shop) | Web App Security | Burp Suite · OWASP ZAP · dirb |
| [Network Reconnaissance Lab](#️-network-reconnaissance-lab) | Recon & Enumeration | Nmap · ARP · dig · Netcat |
| [Honeypot Penetration Testing](#-honeypot-penetration-testing) | Exploitation / Post-Exploitation | Gobuster · Wfuzz · Netcat · Burp Suite |
| [DataTrust – Cyber Infrastructure & Red/Blue Team](#️-datatrust--cyber-infrastructure--redblue-team-exercise) | Infrastructure / Red-Blue Team | Security Onion · Splunk · Kibana · OSSEC |

---

### 🛡️ Vulnerability Assessment – DataTrust

**[→ View Findings](projects/vulnerability-assessment-datatrust/README.md)**

A network and web service vulnerability assessment against a simulated enterprise environment. Full-scope scanning, enumeration, and exploitation across multiple services to identify and validate critical security weaknesses.

**Scope:** Internal network (10.5.1.x) · Apache 2.4.7 · OpenSSH 6.6.1p1 · ProFTPD 1.3.5 · phpMyAdmin · Jetty 8.1.7 · MySQL

| ID | Vulnerability | Severity | CVSS |
|----|--------------|----------|------|
| VA-01 | ProFTPD 1.3.5 Remote Code Execution | 🔴 Critical | 9.8 |
| VA-02 | OpenSSH Authentication Bypass | 🟠 High | 8.2 |
| VA-03 | Apache 2.4.7 Outdated / End-of-Life | 🟠 High | 7.5 |
| VA-04 | phpMyAdmin Exposed — No Access Control | 🟠 High | 7.2 |
| VA-05 | Missing HTTP Security Headers | 🟡 Medium | 5.6 |

**Exploits Demonstrated:**
- OpenSSH brute force via Hydra (CVE-2016-6515)
- Apache Slowloris DoS via Metasploit (CVE-2007-6750)
- phpMyAdmin credential attack (CVE-2020-17530)

`Nmap` `Nikto` `OpenVAS` `Hydra` `Metasploit` `Burp Suite` `OWASP ZAP` `WHOIS`

---

### 🍊 Web Application Security Testing – OWASP Juice Shop

**[→ View Findings](projects/web-application-testing-owasp/README.md)**

End-to-end web application security assessment against the OWASP Juice Shop — a deliberately vulnerable Node.js application. Testing conducted across three difficulty levels covering the OWASP Top 10.

**Key Techniques Demonstrated:**
- SQL injection admin bypass
- DOM-based Cross-Site Scripting (XSS)
- CAPTCHA bypass
- Database schema extraction via UNION-based SQL injection
- Hidden endpoint discovery via automated spider scan
- API manipulation via Burp Suite Repeater
- Password brute force via Burp Suite Intruder

`Burp Suite` `OWASP ZAP` `Browser DevTools` `dirb`

---

### 🛰️ Network Reconnaissance Lab

**[→ View Findings](projects/network-reconnaissance-lab/README.md)**

Structured reconnaissance engagement to identify active hosts, open ports, running services, and potential attack surfaces across a simulated enterprise network.

**Key Techniques Demonstrated:**
- Host discovery via ARP and ICMP
- Full port scan and service version detection with Nmap
- DNS enumeration via nslookup and dig
- Network topology mapping via traceroute
- Service banner grabbing and OS fingerprinting

`Nmap` `ARP` `nslookup` `dig` `traceroute` `Netcat`

---

### 🍯 Honeypot Penetration Testing

**[→ View Findings](projects/honeypot-penetration-testing/README.md)**

Penetration testing of two honeypot virtual machines (HP1VM and HP2VM). Achieved full remote code execution on both targets through different attack chains.

**HP1VM Attack Chain:**
1. Nmap scan → Apache 2.4.38 on port 80 identified
2. Wfuzz → LFI vulnerability discovered in `search1.php`
3. PHP filter exploit → base64-encoded credentials extracted
4. Reverse shell deployed via Netcat listener on port 1234
5. Remote code execution confirmed

**HP2VM Attack Chain:**
1. Gobuster → hidden directories and `.htpasswd` discovered
2. Nikto → file upload vulnerability identified
3. Webshell uploaded via vulnerable upload function
4. Reverse shell deployed → full RCE confirmed

`Nmap` `Nikto` `Gobuster` `Wfuzz` `Netcat` `Burp Suite` `Python`

---

### 🏗️ DataTrust – Cyber Infrastructure & Red/Blue Team Exercise

**[→ View Findings](projects/datatrust-case-study/README.md)**

End-to-end virtualised enterprise security project. Built a 7-VM segmented network from scratch, then conducted full red team exploitation and blue team SOC detection against it.

**Environment:** VirtualBox · 7 VMs · 4 network zones · Security Onion · Splunk · Kali Linux

**Red Team — Exploits Executed:**
- vsftpd 2.3.4 backdoor → root shell (CVE-2011-2523)
- OpenSSH brute force → authenticated access (CVE-2016-6515)
- Apache Slowloris DoS → service outage (CVE-2007-6750)
- SMB port 445 brute force via Legion/Hydra → credential recovery
- XSS execution on OWASP Juice Shop via Burp Suite

**Blue Team — Detection & Monitoring:**
- 9,115 total log events captured across OSSEC, Syslog, Snort, and CRON
- 944 NIDS alerts generated; 803 classified (734 misc activity, 45 potentially bad traffic)
- Port scanning and HTTP exploit traffic detected via Kibana and Squert
- Detection gaps identified and documented for three attack vectors

`Security Onion` `Splunk` `Kibana` `OSSEC` `Snort` `Squert` `Wireshark` `Metasploit` `Legion` `Hydra` `Nmap` `Nikto` `DIRB` `Burp Suite` `OWASP ZAP`

---

> 🖥️ Full network topology, VM configs, and lab ethics — [lab-environment.md](lab-environment.md)  
> 🛠️ Full tool reference and usage notes — [tools-used.md](tools-used.md)

---

## 👤 Author

**Steven Kiprovski** · Sydney, Australia

[![GitHub](https://img.shields.io/badge/GitHub-steve--k--art-181717?style=flat&logo=github&logoColor=white)](https://github.com/steve-k-art)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-steven--kiprovski-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/steven-kiprovski-b6b488387/)
