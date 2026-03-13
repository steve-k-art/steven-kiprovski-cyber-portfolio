# 🛡️ DataTrust Penetration Testing Project  
*Full‑stack penetration test of a simulated enterprise environment*

---

## 📌 1. Project Overview

**Objective:**  
Conduct a full penetration test on DataTrust’s cloned environment, covering reconnaissance, enumeration, vulnerability identification, exploitation, and reporting.

**Scope:**  
- Internal network (10.5.x.x)  
- Apache web server  
- OpenSSH 6.6.1p1  
- phpMyAdmin  
- Honeypot systems  
- OWASP Juice Shop  

**Tools Used:**  
`Nmap`, `ARP`, `nslookup`, `dig`, `traceroute`, `Nikto`, `Hydra`, `BurpSuite`, `ZAP`, `Metasploit`, `Gobuster`, `Wfuzz`, `Python3 HTTP server`

---

# 🛰️ 2. Reconnaissance & Enumeration

## 🔍 2.1 Nmap Network Scan

**Screenshot:**  
![Nmap Scan](screenshots/nmap-scan.png)

**Findings:**  
- DNS service on port 53  
- Only one host active in the scanned range  

---

## 🔍 2.2 ARP Scan

**Screenshot:**  
![ARP Scan](screenshots/arp-scan.png)

**Findings:**  
- Device discovered at 192.168.5.2  
- MAC address successfully resolved  

---

## 🔍 2.3 DNS Enumeration (nslookup & dig)

**Screenshots:**  
![nslookup](screenshots/nslookup.png)  
![dig](screenshots/dig.png)

**Findings:**  
- NXDOMAIN responses  
- No internal DNS records configured  

---

## 🔍 2.4 Traceroute

**Screenshot:**  
![Traceroute](screenshots/traceroute.png)

**Findings:**  
- Single hop to base.example.net  
- ICMP unreachable flags  

---

# ⚠️ 3. Vulnerability Identification

## 3.1 Nikto Scan — Apache Web Server

**Screenshots:**  
![Nikto Scan 1](screenshots/nikto-scan-1.png)
![Nikto Scan 2](screenshots/nikto-scan-2.png)


**Key Findings:**  
- Outdated Apache 2.4.7  
- Directory indexing enabled  
- Missing security headers  
- phpMyAdmin exposed  
- Multiple CVEs detected  

---

## 3.2 Nmap Service Enumeration

**Screenshot:**  
![Nmap Service Scan](screenshots/nmap-service-scan.png)


**Open Ports Identified:**

| Port | Service | Version |
|------|---------|---------|
| 21 | FTP | ProFTPD 1.3.5 |
| 22 | SSH | OpenSSH 6.6.1p1 |
| 80 | HTTP | Apache 2.4.7 |
| 3306 | MySQL | Unauthorized |
| 8080 | Jetty | 8.1.7 |

**Associated Vulnerabilities:**  
- CVE‑2016‑6515 (OpenSSH auth bypass)  
- CVE‑2015‑3306 (ProFTPD RCE)  
- CVE‑2020‑17530 (phpMyAdmin brute‑force)  

---

# 🎯 4. Exploitation Phase

## 4.1 SSH Brute‑Force (Hydra)

**Screenshot:**  
![Hydra SSH Bruteforce](screenshots/hydra-ssh-bruteforce.png)


**Result:**  
- Successful login  
- Username: `vagrant`  
- Password: `vagrant`  

---

## 4.2 SSH Access Confirmation

**Screenshot:**  
![SSH Access](screenshots/ssh-access.png)


**Result:**  
- Full shell access achieved  

---

## 4.3 Apache DoS (Slowloris)

**Screenshot:**  
![Slowloris](screenshots/slowloris.png)

**Result:**  
- Server vulnerable to partial‑request DoS  

---

## 4.4 phpMyAdmin Brute‑Force

**Screenshot:**  
![Hydra phpMyAdmin](screenshots/hydra-phpmyadmin.png)

**Result:**  
- Login vulnerable to brute‑force  
- No rate‑limiting or CAPTCHA  

---

# 🕳️ 5. Honeypot Exploitation

## 5.1 Directory Traversal (LFI)

**Screenshot:**  
![LFI passwd](screenshots/lfi-passwd.png)

**Result:**  
- `/etc/passwd` successfully extracted  

---

## 5.2 Reverse Shell Deployment

**Screenshots:**  
![Python HTTP Server](screenshots/python-http.png)  
![Reverse Shell](screenshots/reverse-shell.png)

**Result:**  
- Remote shell access established  
- Full compromise of honeypot  

---

# 🧩 6. Web Application Attacks (OWASP Juice Shop)

**Screenshots:**  
![DOM XSS](screenshots/dom-xss.png)  
![SQL Injection Login](screenshots/sqli-login.png)  
![CAPTCHA Bypass](screenshots/captcha-bypass.png)  
![Sensitive Data Exposure](screenshots/sensitive-data.png)

**Vulnerabilities Demonstrated:**  
- DOM XSS  
- SQL injection → admin takeover  
- CAPTCHA bypass  
- Sensitive data exposure  
- Broken authentication  

---
---

# 🧾 7. Executive Summary

This penetration test assessed DataTrust’s cloned infrastructure, including internal networks, web applications, authentication services, and honeypot systems. The assessment identified multiple high‑risk vulnerabilities across SSH, Apache, phpMyAdmin, and OWASP Juice Shop, demonstrating weaknesses in authentication, configuration, and access control.

Successful exploitation confirmed that attackers could gain unauthorized access, escalate privileges, extract sensitive data, and disrupt service availability. These findings highlight the need for improved hardening, monitoring, and security controls across the environment.

---

# 🛠️ 8. Recommendations

## 🔐 8.1 Authentication & Access Control
- Enforce strong password policies  
- Implement account lockout and rate‑limiting  
- Disable default credentials  
- Enable MFA where possible  

## 🧱 8.2 Server Hardening
- Update Apache to the latest stable version  
- Install and configure `mod_reqtimeout` and `mod_evasive`  
- Disable directory indexing  
- Restrict access to phpMyAdmin to trusted hosts only  

## 🧪 8.3 Web Application Security
- Implement input validation and sanitization  
- Patch vulnerable components (Jetty, PHP, Apache modules)  
- Add CAPTCHA rate‑limiting and bot‑detection  
- Secure API endpoints with proper authorization checks  

## 🕵️ 8.4 Monitoring & Logging
- Enable centralized log collection  
- Monitor authentication attempts  
- Deploy IDS/IPS rules for Slowloris, brute‑force, and LFI patterns  
- Review honeypot logs regularly to detect attacker behaviour  

## 🛡️ 8.5 Network Security
- Segment critical systems  
- Restrict unnecessary ports  
- Apply firewall rules to limit SSH and phpMyAdmin exposure  
- Conduct regular vulnerability scans  

---

# 🏁 9. Conclusion

The penetration test demonstrated that DataTrust’s environment contains several exploitable vulnerabilities across network services, web applications, and authentication mechanisms. Critical issues such as weak SSH authentication, outdated Apache configurations, exposed phpMyAdmin, and insecure Juice Shop components allowed full system compromise, privilege escalation, and sensitive data exposure.

By implementing the recommended security controls, DataTrust can significantly reduce its attack surface, improve resilience against real‑world threats, and strengthen its overall security posture. This assessment provides a clear roadmap for remediation and future hardening efforts.

---

# 📚 10. Appendix

All screenshots, evidence, and exploitation logs are included in the `/screenshots` and `/screenshots2` directories of this repository.


---


# ✔ End of Case Study 1

