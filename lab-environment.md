# 🖥️ Cybersecurity Lab Environment

All security testing was conducted in an isolated virtual machine environment simulating a real enterprise network. No testing was performed on live or unauthorised systems.

---

## 🏗️ Environment Overview

| Component | Details |
|-----------|---------|
| Virtualisation Platform | VMware Workstation / Oracle VirtualBox |
| Network Type | Host-only / Internal (isolated) |
| Attacker Machine | Kali Linux 2024.3 |
| Target Network Ranges | 10.5.1.x / 10.30.0.x / 192.168.0.x / 192.168.1.x / 192.168.112.x / 192.168.56.x |

---

## ⚔️ Attacker Machines

### Kali Linux 2024.3
Purpose-built penetration testing OS used as the primary attack platform across all projects.

- IP addresses used: `10.5.1.3`, `192.168.0.100`, `192.168.1.100`, `192.168.112.128`, `192.168.56.107`
- Pre-installed toolset including Nmap, Hydra, Metasploit, Nikto, Burp Suite, Legion, and more
- Python HTTP server used to serve payloads to target machines
- Two instances deployed in the DataTrust infrastructure project — one on the Internal network (defensive monitoring) and one on the External Testing network (offensive operations)

---

## 🎯 Target Systems

### DataTrust Security Assessment (10.5.1.137)
Simulated enterprise server running multiple services across a flat network. Used for vulnerability assessment and exploitation.

| Port | Service | Version |
|------|---------|---------|
| 21 | FTP | ProFTPD 1.3.5 |
| 22 | SSH | OpenSSH 6.6.1p1 |
| 80 | HTTP | Apache httpd 2.4.7 |
| 445 | Netbios-SSN | Samba smbd 3.x–4.x |
| 3306 | MySQL | Unauthorized |
| 8080 | HTTP | Jetty 8.1.7 |

---

### DataTrust – Virtualised Infrastructure (10.30.0.0/24)
Full enterprise environment built across 5 isolated network zones for a red/blue team exercise. Designed, implemented, and attacked as part of the DataTrust infrastructure project.

| Device | IP Address | Role |
|--------|-----------|------|
| Security Onion | 192.168.0.1 / 192.168.1.1 / 10.30.0.1 | Centralised firewall, IDS, traffic filtering across all zones |
| Kali Linux (Internal) | 192.168.0.100 | Defensive operations, Wireshark monitoring |
| Kali Linux (External) | 192.168.1.100 | Offensive operations, simulated external attacker |
| Splunk Server | 192.168.0.10 | Centralised log collection and security event analysis |
| Metasploitable 2 | 10.30.0.235 | Honeypot / decoy server — primary red team target |
| Windows Server | 10.30.0.236 | DHCP, DNS, AD Certificate Services, Email |
| Web Server Farm | 10.30.0.237 | OWASP Juice Shop hosted on port 3000 |

**Network Zones:**

| Zone | Subnet | Purpose |
|------|--------|---------|
| Internal Network | 192.168.0.0/24 | Defensive operations, log collection |
| External Testing Network | 192.168.1.0/24 | Simulated external attacker |
| DMZ (Perimeter) | 10.30.0.0/24 | Public-facing services, honeypot |
| ISP (Internet Simulation) | 10.0.2.x | Untrusted external traffic |

---

### OWASP Juice Shop (127.0.0.1:3000)
Deliberately insecure Node.js web application used for web application security testing.

- Hosted locally on Kali Linux via Docker
- Tested across three difficulty levels
- Proxy traffic intercepted via Burp Suite on `localhost:8080`
- Also deployed on Web Server Farm (10.30.0.237:3000) during the DataTrust infrastructure project

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
   _____|______________________________________________
   |              |              |                   |
[DataTrust]  [Juice Shop]   [HP1VM]              [HP2VM]
10.5.1.137  localhost:3000  192.168.112.130    192.168.56.110


DataTrust Infrastructure Project — 5-Zone Architecture:

[ISP / Internet Simulation - 10.0.2.x]
              |
      [Security Onion] ← Centralised firewall, IDS, router
       /       |        \
      /        |         \
[Internal]   [DMZ]   [External Testing]
192.168.0.x  10.30.0.x  192.168.1.x
(Splunk,    (Metasploitable2,  (Kali —
 Kali)       Windows Server,   offensive
             Juice Shop)       operations)
```

---

## ✅ Lab Safety & Ethics

- All testing was performed exclusively within the isolated virtual lab environment
- No external or production systems were targeted at any point
- All activities were conducted in accordance with DataTrust's simulated WHS policy
- Tools were used solely for educational and assessment purposes within the Advanced Diploma of Cyber Security program
- All virtual machines were isolated using host-only or internal network adapters to prevent any unintended external traffic
