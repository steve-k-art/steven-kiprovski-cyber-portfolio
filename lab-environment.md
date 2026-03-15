# 🛠️ Cybersecurity Tools Used

A reference guide to the tools used across all projects in this portfolio, including their purpose and how they were applied.

---

## 🖥️ Operating System

### Kali Linux
Primary operating system used for all penetration testing and vulnerability assessment activities. Provides a purpose-built environment with pre-installed security tools.

---

## 🔍 Reconnaissance & Network Scanning

### Nmap
Used for network discovery, host identification, port scanning, and service version detection (`-sV`). Applied across all projects to map the target environment and identify open ports and running services. NSE scripts used for banner grabbing, default credential checks, and CVE-based vulnerability scanning.

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

### Legion
Used for automated network scanning and service enumeration combined with credential brute-forcing. Applied during the DataTrust infrastructure red team exercise against SMB (port 445) on the honeypot target to discover and exploit weak credentials.

---

## 🌐 Web Application Testing

### Burp Suite
Used to intercept, inspect, and manipulate HTTP/HTTPS requests and responses. Applied extensively in OWASP Juice Shop testing for SQL injection, CAPTCHA bypass, password brute force via Intruder, and API endpoint manipulation via Repeater. Also used during the DataTrust infrastructure project for XSS payload delivery.

### OWASP ZAP
Used to perform automated spider scans and active/passive vulnerability assessments. Applied against OWASP Juice Shop to discover the admin email address and identify hidden endpoints. Also used during the DataTrust infrastructure project to generate full web application vulnerability reports.

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
Used to perform brute-force credential attacks against multiple services. Applied against SSH (CVE-2016-6515) and phpMyAdmin (CVE-2020-17530) in the DataTrust vulnerability assessment. Also applied against SMB port 445 during the DataTrust infrastructure red team exercise.

### Metasploit Framework
Used to test exploitation of identified vulnerabilities. Applied to execute the Slowloris DoS module (`auxiliary/dos/http/slowloris`) against Apache HTTP Server (CVE-2007-6750). Also used to exploit vsftpd 2.3.4 backdoor (CVE-2011-2523) for root shell access during the infrastructure red team exercise.

### Python HTTP Server
Used to serve malicious payloads (reverse shell scripts) to target machines during the Honeypot lab. Launched via `python3 -m http.server 80`.

---

## 🔎 Vulnerability Scanning

### Nikto
Used to scan web servers for vulnerabilities, outdated software versions, missing security headers, and exposed configuration files. Applied against the DataTrust Apache server, both honeypot VMs, and the Metasploitable 2 target during the infrastructure project.

### OpenVAS
Used for comprehensive, authenticated vulnerability scanning across the DataTrust environment. Identified service-level CVEs, misconfigurations, and risk-rated findings across multiple targets.

---

## 🖧 Network Security & Monitoring

### Security Onion
Used as a centralised firewall, router, and network IDS platform during the DataTrust infrastructure project. Configured with four network interfaces to segment the Internal, DMZ, External Testing, and ISP zones. Provided centralised traffic filtering and IDS alerting across all zones.

### Splunk
Used for centralised log collection, indexing, and security event analysis. Configured to ingest logs from across the virtualised enterprise environment. Integrated with Kibana for dashboard visualisation and event timeline analysis.

### OSSEC (HIDS)
Host-based intrusion detection system deployed during the DataTrust infrastructure project. Generated real-time alerts for port status changes and zero-packet events during red team testing. Logs reviewed via Kibana dashboard showing 9,115 total events captured.

### Snort
Network-based IDS configured with custom detection rules during the DataTrust infrastructure project. Rules written to detect ICMP flooding and port scanning activity. Configured to send automated email alerts to the security team upon trigger.

### Wireshark
Used for packet-level traffic capture and analysis. Applied to monitor live traffic into the honeypot during the infrastructure project, capturing ICMP and TCP packets from the external testing machine. Also useful for identifying unencrypted credentials and protocol-level vulnerabilities.

---

## 📊 Log Analysis & Visualisation

### Kibana
Used to visualise and analyse security event logs via dashboards during the DataTrust infrastructure project. Tracked 9,115 OSSEC and syslog events, 944 NIDS alerts, and 803 classified threat events. Used to identify activity spikes and correlate attack timelines.

### Squert
Used for IDS event analysis and timeline visualisation during the DataTrust infrastructure blue team exercise. Detected VNC scan attempts (ET SCAN 2002910) and logged 533 listened port status events. Provided priority-based filtering for event triage.

---

## 📋 Supporting Tools

| Tool | Purpose |
|------|---------|
| `netdiscover` | Active host discovery on local networks |
| `WHOIS` | Passive information gathering on domain registration |
| `ssh` | Remote shell access after credential discovery |
| `ip a` | Network interface enumeration on attacker machine |
| `uname` | OS identification on compromised machines |
| `iptables` | Firewall rule configuration on Linux systems — used to block SSH (port 22) and permit HTTP (port 80) during infrastructure hardening |
| `docker` | Used to deploy OWASP Juice Shop container (`docker run --rm -p 3000:3000 bkimminich/juice-shop`) |
