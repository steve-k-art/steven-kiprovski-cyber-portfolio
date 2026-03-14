# 🛰️ Network Reconnaissance Lab  
*Network discovery, enumeration, and service identification in a controlled lab environment*

---

## 📌 1. Project Overview

**Objective:**  
Perform structured network reconnaissance to identify active hosts, open ports, running services, and potential attack surfaces within a simulated enterprise environment.

**Focus Areas:**  
- Host discovery  
- Service enumeration  
- DNS analysis  
- Network path tracing  
- Evidence‑based reporting  

**Tools Used:**  
`Nmap`, `ARP`, `nslookup`, `dig`, `traceroute`, `Netcat`, `WHOIS`

---

# 🛰️ 2. Reconnaissance & Enumeration

## 🔍 2.1 Nmap Host Discovery

![Nmap Scan](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/nmap-scan.png)

**Findings:**  
- Identified active hosts within the 192.168.x.x range  
- Detected ICMP echo responses  
- Confirmed network accessibility and baseline topology  

---

## 🔍 2.2 ARP Scan

![ARP Scan](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/arp-scan.png)

**Findings:**  
- Discovered local devices using ARP broadcast  
- Successfully resolved MAC addresses  
- Identified gateway and internal hosts  

---

## 🔍 2.3 DNS Enumeration (nslookup & dig)

![nslookup](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/nslookup.png)  
![dig](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/dig.png)

**Findings:**  
- No internal DNS records configured  
- NXDOMAIN responses indicate minimal DNS footprint  
- Useful for confirming lack of internal name resolution  

---

## 🔍 2.4 Traceroute

![Traceroute](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/traceroute.png)

**Findings:**  
- Single hop to internal host  
- ICMP unreachable flags observed  
- Confirms flat network structure  

---

## 🔍 2.5 Service Enumeration (Nmap -sV)

![Nmap Service Scan](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots/nmap-service-scan.png)

**Open Ports Identified:**

| Port | Service | Version |
|------|---------|---------|
| 22 | SSH | OpenSSH 6.x |
| 80 | HTTP | Apache 2.x |
| 3306 | MySQL | Unauthorized |
| 8080 | Jetty | 8.x |

**Insights:**  
- Multiple outdated services  
- Potential attack surface for future exploitation  
- Confirms environment suitable for vulnerability assessment  

---

# ⚠️ 3. Key Observations
- Flat network structure increases lateral movement risk  
- Outdated services detected (Apache, SSH, Jetty)  
- Minimal DNS infrastructure  
- No IDS/IPS interference detected  

---

# 🧩 4. Skills Demonstrated
- Network scanning & host discovery  
- Service enumeration & version detection  
- DNS interrogation  
- Network path analysis  
- Evidence collection & documentation  
- Interpreting reconnaissance data to identify potential risks  

---

# 🛠️ 5. Recommendations

### 🧱 Network Hardening  
- Implement segmentation between user, server, and management networks  
- Restrict unnecessary ports and services  

### 🔐 Service Security  
- Update outdated services  
- Disable unused services  
- Enforce secure configurations  

### 🕵️ Monitoring  
- Deploy IDS/IPS  
- Enable logging for DNS, SSH, and HTTP services  

---

# 🏁 6. Conclusion
This Network Reconnaissance Lab demonstrates foundational security testing skills, including host discovery, service enumeration, DNS analysis, and network mapping. The results highlight several outdated services and a flat network structure, both of which increase the attack surface.

---

# 📚 7. Appendix

![Reverse Shell](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/honeypot-reverse-shell.png)

![Hydra phpMyAdmin](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/hydra-phpmyadmin.png)

![CAPTCHA Bypass](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-captcha-bypass.png)

![DOM XSS](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-dom-xss.png)

![Sensitive Data](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sensitive-data.png)

![SQL Login](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sql-login.png)

![LFI passwd](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/lfi-passwd.png)

![Slowloris DoS](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/slowloris-dos.png)
