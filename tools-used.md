# 🛠️ Cybersecurity Tools Used

A reference guide to the tools used across all projects in this portfolio, including their purpose and how they were applied.

---

## 🖥️ Operating System

### Kali Linux
Primary operating system used for all penetration testing and vulnerability assessment activities. Provides a purpose-built environment with pre-installed security tools.

---

## 🔍 Reconnaissance & Network Scanning

### Nmap
Used for network discovery, host identification, port scanning, and service version detection (`-sV`). Applied across all projects to map the target environment and identify open ports and running services.

### ARP
Used to discover active devices on local networks by resolving IP addresses to MAC addresses. Applied during the Network Reconnaissance Lab to confirm host availability.

### nslookup
Used to query DNS for domain-to-IP resolution. Applied to confirm DNS configuration and identify the absence of internal name resolution in the DataTrust environment.

### dig
Versatile DNS querying tool used to interrogate DNS records in detail. Provides deeper insight than nslookup, useful for identifying DNS misconfigurations.

### traceroute
Used to trace the network path packets take to reach a target. Applied to map network topology and confirm flat network structure in the DataTrust environment.

### Netcat (nc)
Used to set up listeners for incoming reverse shell connections. Applied in the Honeypot lab to receive a reverse shell from the target machine on port 1234.

---

## 🌐 Web Application Testing

### Burp Suite
Used to intercept, inspect, and manipulate HTTP/HTTPS requests and responses. Applied extensively in OWASP Juice Shop testing for SQL injection, CAPTCHA bypass, password brute force via Intruder, and API endpoint manipulation via Repeater.

### OWASP ZAP
Used to perform automated spider scans against the OWASP Juice Shop web application. Discovered the admin email address and identified hidden endpoints for further exploitation.

### Browser DevTools
Used to inspect the DOM structure of web pages during XSS testing. Applied to locate the iframe element that confirmed the DOM-based XSS vulnerability in Juice Shop.

### dirb
Used to brute-force hidden web directories and files. Applied in the Honeypot lab to discover upload directories used for webshell deployment.

### Wfuzz
Used to fuzz web application parameters for Local File Inclusion (LFI) vulnerabilities. Applied in the Honeypot lab to discover the vulnerable `search1.php` parameter.

### Gobuster
Used for fast directory and file enumeration against web servers. Applied in the Honeypot lab to identify sensitive files including `.htaccess`, `.htpasswd`, and `index.php`.

---

## 💥 Exploitation & Attack Tools

### Hydra
Used to perform brute-force credential attacks against multiple services. Applied against SSH (CVE-2016-6515) and phpMyAdmin (CVE-2020-17530) in the DataTrust assessment.

### Metasploit Framework
Used to test exploitation of identified vulnerabilities. Applied to execute the Slowloris DoS module (`auxiliary/dos/http/slowloris`) against Apache HTTP Server (CVE-2007-6750).

### Python HTTP Server
Used to serve malicious payloads (reverse shell scripts) to target machines during the Honeypot lab. Launched via `python3 -m http.server 80`.

---

## 🔎 Vulnerability Scanning

### Nikto
Used to scan web servers for vulnerabilities, outdated software versions, missing security headers, and exposed configuration files. Applied against the DataTrust Apache server and both honeypot VMs.

---

## 📡 Traffic Analysis

### Wireshark
Used for analysing network traffic and inspecting packet captures. Useful for identifying unencrypted credentials, malicious traffic patterns, and protocol-level vulnerabilities.

---

## 📋 Supporting Tools

| Tool | Purpose |
|------|---------|
| `netdiscover` | Active host discovery on local networks |
| `WHOIS` | Passive information gathering on domain registration |
| `ssh` | Remote shell access after credential discovery |
| `ip a` | Network interface enumeration on attacker machine |
| `uname` | OS identification on compromised machines |
