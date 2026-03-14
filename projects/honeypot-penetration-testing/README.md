# 🍯 Honeypot Security Infrastructure – Penetration Testing  
*Exploitation of two honeypot VMs including LFI, reverse shell, and PHP filter attacks*

---

## 📌 1. Project Overview

**Objective:**  
Perform penetration testing against DataTrust's honeypot security infrastructure across two virtual machines (HP1VM and HP2VM), demonstrating real-world exploitation techniques including local file inclusion, reverse shell deployment, and PHP filter-based credential extraction.

**Scope:**  
- Honeypot VM 1 (HP1VM) — IP: 192.168.112.130  
- Honeypot VM 2 (HP2VM) — IP: 192.168.56.110  
- Attacker machine (Kali Linux)  

**Tools Used:**  
`Nmap`, `Nikto`, `Gobuster`, `Wfuzz`, `dirb`, `Netcat`, `Burp Suite`, `Python HTTP Server`

---

# 🧪 2. Honeypot 1 (HP1VM)

**Environment Setup:**  
- Attacker IP: 192.168.112.128 (Kali)  
- Target IP: 192.168.112.130 (HP1VM)  
- Target discovered using `netdiscover`  

---

## 🔍 2.1 Network Scanning

**Nmap basic scan** revealed ports 22 (SSH) and 80 (HTTP) open on the target.

**Deeper service scan** identified:  
- Port 80/tcp — Apache httpd 2.4.38 (Debian)  
- Web application actively serving content  

---

## 🔍 2.2 Directory Enumeration (Gobuster)

**Method:**  
Ran Gobuster against the target web server to enumerate hidden directories and files.

**Findings:**  
- `/account` directory discovered  
- `index.php` identified — confirms PHP technology stack  
- `.htaccess` and `.htpasswd` files found (protected but notable)  
- Sensitive areas identified for further investigation  

---

## 💥 2.3 Local File Inclusion (LFI) – /etc/passwd

![LFI passwd](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/lfi-passwd.png)

**Method:**  
Used Wfuzz to fuzz for valid parameters vulnerable to Local File Inclusion. Discovered vulnerable endpoint:  
`http://192.168.112.130/search1.php?FUZZ=me`

Then exploited the LFI to read the system password file:  
`http://192.168.112.130/search1.php?me=/etc/passwd`

**Result:**  
- Full contents of `/etc/passwd` retrieved  
- Multiple system user accounts disclosed  
- Confirms directory traversal / LFI vulnerability in `search1.php`  

---

## 💥 2.4 Reverse Shell Deployment

![Reverse Shell](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/honeypot-reverse-shell.png)

**Method:**  
1. Created a custom `reverse_shell.php` script using `fsockopen()` and `proc_open()` to connect back to the attacker machine  
2. Served the script via Python HTTP server on Kali: `python3 -m http.server 80`  
3. Set up a Netcat listener: `nc -lvnp 1234`  
4. Triggered the reverse shell via the web server  

**Result:**  
- Connection received from 192.168.112.130 on port 1234  
- Shell established as `www-data`  
- OS confirmed as Linux via `uname` command  
- Full remote command execution achieved on target  

---

# 🧪 3. Honeypot 2 (HP2VM)

**Environment Setup:**  
- Attacker IP: 192.168.56.107 (Kali)  
- Target IP: 192.168.56.110 (HP2VM)  
- Connectivity confirmed via ping  

---

## 🔍 3.1 Network Scanning (Nmap -A)

**Aggressive scan findings:**

| Port | Service | Version | Notes |
|------|---------|---------|-------|
| 80 | HTTP | Apache 2.4.10 (Debian) | PwnLab Intranet Image Hosting |
| 111 | RPCBind | 2–4 | Potential info disclosure |
| 3306 | MySQL | 5.5.47 | High-value target |

---

## 🔍 3.2 Nikto Web Server Scan

**Key Findings:**  
- Apache 2.4.10 is outdated (minimum 2.4.54)  
- X-Frame-Options header missing — clickjacking risk  
- X-Content-Type-Options not set  
- Internal IP 127.0.0.1 disclosed via `/images` directory (CVE-2000-0649)  
- PHPSESSID cookie missing `httponly` flag — XSS risk  
- Directory indexing enabled on `/images/`  
- `config.php` identified — potential database credential exposure  
- `/login.php` admin login page discovered  

---

## 💥 3.3 PHP Filter Exploit – Credential Extraction

**Method:**  
Exploited a PHP file inclusion vulnerability using the `php://filter` wrapper to encode sensitive files as Base64:  
`http://192.168.56.110/?page=php://filter/convert.base64-encode/resource=config`

Decoded the returned Base64 string on Kali to reveal plaintext credentials from `config.php`.

**Result:**  
- Database credentials extracted:  
  - Username: `root`  
  - Password: `H4u%QJ_H99`  
- Demonstrates Remote File Inclusion (RFI) / PHP filter vulnerability  

---

## 💥 3.4 Webshell Upload & Reverse Shell

**Method:**  
1. Created a Python-based reverse shell script  
2. Opened a Netcat listener on Kali  
3. Used `dirb` to discover a hidden upload directory  
4. Intercepted a GET request in Burp Suite and manipulated it to include the Python reverse shell  
5. Forwarded the manipulated request to the server  

**Result:**  
- Reverse shell successfully executed  
- Full remote access gained to HP2VM  
- Demonstrates combined Burp manipulation + webshell upload attack chain  

---

# ⚠️ 4. Key Findings

| ID | VM | Vulnerability | Severity | Evidence |
|----|----|--------------|----------|----------|
| HP-01 | HP1VM | Local File Inclusion (LFI) | Critical | lfi-passwd |
| HP-02 | HP1VM | Remote Code Execution via Reverse Shell | Critical | honeypot-reverse-shell |
| HP-03 | HP2VM | PHP Filter Credential Exposure | Critical | config.php decode |
| HP-04 | HP2VM | Webshell Upload + RCE | Critical | Burp + dirb |
| HP-05 | HP2VM | Outdated Apache 2.4.10 | High | Nikto scan |
| HP-06 | HP2VM | MySQL 5.5.47 Exposed | High | Nmap scan |
| HP-07 | HP2VM | Missing Security Headers | Medium | Nikto scan |
| HP-08 | HP2VM | Directory Indexing Enabled | Medium | Nikto scan |

---

# 🛠️ 5. Recommendations

### 🔐 File Inclusion Prevention  
- Disable `allow_url_include` and `allow_url_fopen` in `php.ini`  
- Validate and whitelist all user-supplied file path parameters  
- Never pass user input directly to file system functions  

### 🧱 Server Hardening  
- Update Apache to current stable version (2.4.54+)  
- Restrict PHP `php://filter` wrapper usage in production  
- Disable directory indexing in Apache configuration  
- Move `config.php` outside of web root or restrict access  

### 🔒 Web Application Security  
- Implement proper output encoding and CSP headers  
- Add `httponly` and `secure` flags to all session cookies  
- Restrict file upload types and scan uploaded files  
- Add `X-Frame-Options` and `X-Content-Type-Options` headers  

### 🕵️ Monitoring  
- Monitor for unusual outbound connections from web server processes  
- Alert on Netcat or reverse shell patterns in network traffic  
- Log all PHP errors and file access attempts  

---

# 🏁 6. Conclusion

The honeypot penetration tests demonstrated critical vulnerabilities across both VMs. On HP1VM, a Local File Inclusion vulnerability allowed disclosure of system users and ultimately full remote code execution via a reverse shell. On HP2VM, a PHP filter exploit revealed database credentials in plaintext, and a webshell upload achieved complete system compromise. These findings underscore the severity of file inclusion vulnerabilities and the importance of hardening PHP configurations and web application input validation.

---

# 📚 7. Appendix

![LFI passwd](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/lfi-passwd.png)

![Reverse Shell](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/honeypot-reverse-shell.png)

