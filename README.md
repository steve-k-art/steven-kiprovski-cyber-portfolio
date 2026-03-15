# Steven Kiprovski – Cybersecurity Portfolio

Welcome to my cybersecurity portfolio. This repository demonstrates hands-on security testing projects completed during my **Advanced Diploma of Cyber Security**, conducted entirely within isolated virtual lab environments.

---

## 🧠 Skills Demonstrated

- Network Reconnaissance & Host Discovery
- Vulnerability Assessment & CVE Analysis
- Web Application Security Testing
- Penetration Testing & Exploit Implementation
- Security Risk Analysis & Remediation Reporting
- Tool Proficiency: `Nmap`, `Nikto`, `Hydra`, `Metasploit`, `Burp Suite`, `OWASP ZAP`, `Netcat`, `Wfuzz`, `Gobuster`

---

## 📁 Projects

### 🛡️ [Vulnerability Assessment – DataTrust](projects/vulnerability-assessment-datatrust/README.md)
Comprehensive penetration test against a simulated enterprise environment. Identified and exploited three CVEs including OpenSSH brute force (CVE-2016-6515), Apache Slowloris DoS (CVE-2007-6750), and phpMyAdmin credential attack (CVE-2020-17530). Includes full remediation report.

**Tools:** `Nmap` `Nikto` `Hydra` `Metasploit` `ARP` `traceroute`

---

### 🍊 [Web Application Security Testing – OWASP Juice Shop](projects/web-application-testing-owasp/README.md)
End-to-end web application security assessment across three difficulty levels. Demonstrated SQL injection admin bypass, DOM-based XSS, CAPTCHA bypass, database schema extraction via UNION injection, and proxy-based vulnerability assessment.

**Tools:** `Burp Suite` `OWASP ZAP` `Browser DevTools` `dirb`

---

### 🛰️ [Network Reconnaissance Lab](projects/network-reconnaissance-lab/README.md)
Structured network reconnaissance to identify active hosts, open ports, running services, and potential attack surfaces across a simulated enterprise network. Includes DNS enumeration, traceroute analysis, and full service version detection.

**Tools:** `Nmap` `ARP` `nslookup` `dig` `traceroute` `Netcat`

---

### 🍯 [Honeypot Penetration Testing](projects/honeypot-penetration-testing/README.md)
Penetration testing of two honeypot virtual machines. Achieved remote code execution via Local File Inclusion, reverse shell deployment, PHP filter-based credential extraction, and webshell upload across two target VMs.

**Tools:** `Nmap` `Nikto` `Gobuster` `Wfuzz` `Netcat` `Burp Suite` `Python`

---

### 🏗️ [DataTrust – Cyber Infrastructure & Red/Blue Team Exercise](projects/datatrust-infrastructure-pentest/README.md)
Designed and attacked a full virtualised enterprise environment across 5 network zones. 
Red team exploitation of 5+ CVEs, blue team detection via Splunk/Kibana/OSSEC, 
revised risk assessment and remediation roadmap.

## 🖥️ Lab Environment

All testing was performed in an isolated virtual machine environment — no live or unauthorised systems were targeted. See [lab-environment.md](lab-environment.md) for full details.

| Component | Details |
|-----------|---------|
| Attacker | Kali Linux 2024.3 |
| Virtualisation | VMware Workstation / VirtualBox |
| Targets | DataTrust server, OWASP Juice Shop, HP1VM, HP2VM |
| Network | Host-only / Internal (isolated) |

---

## 🛠️ Tools Reference

For a full breakdown of every tool used and how it was applied, see [tools-used.md](tools-used.md).

---

## 📜 Certification

**Advanced Diploma of Cyber Security**  
Practical coursework covering penetration testing methodologies, network security, web application security, and security infrastructure evaluation.

---

## 👤 Author

**Steven Kiprovski**  
Sydney, Australia  
🔗 [github.com/steve-k-art](https://github.com/steve-k-art)

