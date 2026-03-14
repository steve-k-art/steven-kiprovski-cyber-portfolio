# 🖥️ Cybersecurity Lab Environment

All security testing was conducted in an isolated virtual machine environment simulating a real enterprise network. No testing was performed on live or unauthorised systems.

---

## 🏗️ Environment Overview

| Component | Details |
|-----------|---------|
| Virtualisation Platform | VMware Workstation / Oracle VirtualBox |
| Network Type | Host-only / Internal (isolated) |
| Attacker Machine | Kali Linux 2024.3 |
| Target Network Ranges | 10.5.1.x / 192.168.112.x / 192.168.56.x |

---

## ⚔️ Attacker Machine

### Kali Linux 2024.3
Purpose-built penetration testing OS used as the primary attack platform across all projects.

- IP addresses used: `10.5.1.3`, `192.168.112.128`, `192.168.56.107`
- Pre-installed toolset including Nmap, Hydra, Metasploit, Nikto, Burp Suite, and more
- Python HTTP server used to serve payloads to target machines

---

## 🎯 Target Systems

### DataTrust Security Infrastructure (10.5.1.137)
Simulated enterprise server running multiple services across a flat network.

| Port | Service | Version |
|------|---------|---------|
| 21 | FTP | ProFTPD 1.3.5 |
| 22 | SSH | OpenSSH 6.6.1p1 |
| 80 | HTTP | Apache httpd 2.4.7 |
| 445 | Netbios-SSN | Samba smbd 3.x–4.x |
| 3306 | MySQL | Unauthorized |
| 8080 | HTTP | Jetty 8.1.7 |

---

### OWASP Juice Shop (127.0.0.1:3000)
Deliberately insecure Node.js web application used for web application security testing.

- Hosted locally on Kali Linux
- Tested across three difficulty levels
- Proxy traffic intercepted via Burp Suite on `localhost:8080`

---

### Honeypot VM 1 – HP1VM (192.168.112.130)
Linux web server running a vulnerable PHP web application.

| Port | Service | Version |
|------|---------|---------|
| 22 | SSH | OpenSSH |
| 80 | HTTP | Apache httpd 2.4.38 (Debian) |

- Vulnerable to Local File Inclusion via `search1.php`
- Exploited via reverse shell connecting back to Kali on port 1234

---

### Honeypot VM 2 – HP2VM (192.168.56.110)
PwnLab Intranet Image Hosting server running a vulnerable PHP application.

| Port | Service | Version |
|------|---------|---------|
| 80 | HTTP | Apache 2.4.10 (Debian) |
| 111 | RPCBind | 2–4 |
| 3306 | MySQL | 5.5.47 |

- Vulnerable to PHP filter exploit revealing database credentials
- Exploited via webshell upload and reverse shell

---

### Base Network VM (10.5.1.1)
Internal DNS and network base machine used as part of the DataTrust security infrastructure simulation.

- Running domain service on port 53/tcp
- Confirmed via Nmap scan and traceroute (single hop)

---

## 🌐 Network Topology

```
[ Kali Linux - Attacker ]
        |
        | Host-only / Internal Network
        |
   _____|______________________________________
   |              |              |            |
[DataTrust]  [Juice Shop]  [HP1VM]        [HP2VM]
10.5.1.137  localhost:3000  192.168.112.130  192.168.56.110
```

---

## ✅ Lab Safety & Ethics

- All testing was performed exclusively within the isolated virtual lab environment
- No external or production systems were targeted
- All activities were conducted in accordance with DataTrust's simulated WHS policy
- Tools were used solely for educational and assessment purposes within the Advanced Diploma of Cyber Security program
