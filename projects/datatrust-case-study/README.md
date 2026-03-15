# DataTrust Cybersecurity Infrastructure & Penetration Testing — Case Study

**Steven Kiprovski | Advanced Diploma of Cyber Security**  
**Project:** ICTCYS612 · ICTCYS608 — Virtualised Cyber Security Infrastructure & Risk Assessment  

---

## Executive Summary

This project involved designing, building, and attacking a virtualised enterprise cybersecurity infrastructure for a simulated organisation called DataTrust — a mid-sized company handling sensitive client data, financial records, and employee PII. The engagement covered the full security lifecycle: risk assessment, infrastructure design, implementation, active red/blue team testing, and a revised remediation plan.

The environment was built entirely within isolated virtual machines using industry-standard tooling. No live or unauthorised systems were targeted at any point.

> **Outcome:** Multiple critical vulnerabilities were identified and successfully exploited during red team operations. Detection gaps were identified in the blue team response. A revised risk assessment and remediation roadmap were produced for the client.

---

## Scope & Environment

| Component | Details |
|-----------|---------|
| Attacker Machines | Kali Linux 2024.3 (x2 — Internal & External testing networks) |
| Virtualisation | VMware Workstation / VirtualBox |
| Firewall / Router | Security Onion (centralised gateway) |
| Monitoring | Splunk, Kibana, Squert, Wireshark, OSSEC HIDS |
| Targets | Metasploitable 2 (Honeypot), Windows Server, OWASP Juice Shop |
| Network Zones | Internal (192.168.0.0/24), External Testing (192.168.1.0/24), DMZ (10.30.0.0/24) |

### Network Architecture

```
[ISP / Internet Simulation]
        |
  [Security Onion] ← Centralised firewall, IDS, traffic filtering
   /      |       \
Internal  DMZ    External Testing
Network   Zone   Network
(Splunk, (Metasploitable2, (Kali — offensive
 Kali)    Windows Server,   operations)
          Juice Shop)
```

**Why this matters for employers:** This architecture mirrors real-world segmented enterprise environments — isolated zones, a DMZ for public-facing services, and an internal monitoring network. It demonstrates the ability to think in network boundaries, not just individual machines.

---

## Initial Risk Assessment

The following vulnerabilities were identified prior to testing and risk-rated against DataTrust's defined risk appetite (low tolerance for high-impact, data-exposing vulnerabilities).

| Vulnerability | CVE(s) | Impact | Risk Rating | Relevant Legislation |
|---------------|--------|--------|-------------|----------------------|
| Social Engineering (Phishing) | N/A | Credential exposure → unauthorised access | **High** | Crimes Act 1990 (NSW); Criminal Code Act 1995 (Cth); Privacy Act 1988 |
| ETERNALBLUE — SMBv1 RCE | CVE-2017-0144 | Full system compromise, sensitive data exposure | **Extreme** | Criminal Code Act 1995; Privacy Act 1988; Security of Critical Infrastructure Act 2018 |
| Unpatched Systems (ProFTPD / OpenSSH) | CVE-2015-3306, CVE-2016-6515 | Remote code execution → system compromise | **High** | Privacy Act 1988; Security of Critical Infrastructure Act 2018 |
| SChannel Vulnerability | CVE-2014-6321 | DoS via crafted code over SChannel | **High** | Security of Critical Infrastructure Act 2018; Privacy Act 1988 |
| Weak Password Policy | N/A | Brute-force → unauthorised access | **High** *(escalated from Medium after stakeholder review)* | Privacy Act 1988; Criminal Code Act 1995 |
| HSTS Not Enforced | CVE-2014-3566 (POODLE) | MITM — interception of sensitive data in transit | **Medium** | Privacy Act 1988; Telecommunications Act 1997 |
| Apache HTTPD MITM | CVE-2016-4975 | Unauthorised access to internal communications | **Medium** | Privacy Act 1988; Telecommunications Act 1997 |
| Cookie Missing HttpOnly Attribute | N/A | XSS / CSRF exposure | **Medium** | Privacy Act 1988; Criminal Code Act 1995 |

> **Note on risk escalation:** The weak password policy was initially rated Medium. After stakeholder feedback identified widespread use of simple passwords across systems, the risk rating was escalated to High — demonstrating the ability to incorporate organisational feedback into live risk assessments, a core GRC competency.

---

## Infrastructure Implementation

### Security Zone Design

Five distinct network zones were created to mirror real enterprise segmentation:

- **Internal Network** — Defensive operations, log collection (Splunk), workstation monitoring
- **DMZ (Perimeter Network)** — Publicly accessible services (Juice Shop), honeypot (Metasploitable 2), Windows Server
- **External Testing Network** — Simulates external threat actors performing offensive operations
- **Security Zone (Gateway)** — Security Onion acting as centralised firewall and IDS
- **Management Zone** — Core service access with elevated monitoring

### Key Technologies Deployed

| Security Need | Technology | Purpose |
|---------------|-----------|---------|
| Access Control | MFA + RBAC | Restrict sensitive system access to authorised users |
| Data Encryption | AES-256 | Protect data at rest and in transit |
| Network Segmentation | VLANs | Limit lateral movement after a breach |
| Intrusion Detection | OSSEC HIDS + Snort | Real-time threat detection and alerting |
| Log Management | Splunk + Kibana | Centralised log collection, analysis, and visualisation |
| Penetration Testing | Kali Linux suite (Metasploit, Nmap, Hydra, Burp Suite, OWASP ZAP) | Simulated offensive operations |
| Disaster Recovery | Automated backup (Veeam) | Business continuity after attack or failure |

### Firewall Configuration (Security Onion — OPNsense)

- Inbound: HTTPS (443) and SMTP (25) permitted; all other inbound blocked by default
- Outbound: Restricted to essential services; strict controls to prevent data exfiltration
- IP forwarding enabled between zones with explicit routing rules
- SSH (port 22) blocked via iptables; HTTP (port 80) permitted for web services

---

## Vulnerability Scan Findings — Nmap / Nikto / DIRB

A comprehensive scan of the target environment (Metasploitable 2 at `10.30.0.235`) using Nmap with NSE scripts, Nikto, and DIRB identified the following:

### Critical Services & Associated CVEs

| Service | Version | CVE | Risk |
|---------|---------|-----|------|
| FTP (vsftpd) | 2.3.4 | CVE-2011-2523 — backdoor allowing RCE via crafted FTP session | Critical |
| SSH (OpenSSH) | 4.7p1 | CVE-2008-5161 — buffer overflow → arbitrary code execution | High |
| SSH (OpenSSH) | 4.7p1 | CVE-2009-2904 — DoS via improper SSH2 message handling | High |
| Telnet | — | CVE-2002-1047 — plaintext comms; remote code/info exposure | High |
| Apache HTTP | 2.2.8 | CVE-2007-6750 — Slowloris DoS via partial HTTP requests | High |
| Apache HTTP | 2.2.8 | CVE-2009-3555 — SSL renegotiation; arbitrary data injection | High |
| Samba (SMB) | 3.0.20 | CVE-2009-3134 — RCE via crafted RPC request | Critical |
| Samba (SMB) | 3.0.20 | CVE-2017-7494 — shared library upload → server-side execution | Critical |
| MySQL | Unknown | CVE-2006-5873 — improper input handling → RCE | High |
| PostgreSQL | 8.3.0–8.3.7 | CVE-2009-3230 — unauthorised access / privilege escalation | High |
| VNC | 3.3 | CVE-2006-5830 — keystroke capture, server access | High |
| RPC (rpcbind) | — | CVE-2007-2447 — RCE if exploited via NFS service | High |

### Web Application Findings (Nikto / DIRB)

- **Missing security headers:** X-Frame-Options and X-Content-Type-Options absent — exposure to clickjacking and MIME-sniffing attacks
- **TRACE method enabled** — Cross-Site Tracing (XST) vulnerability
- **phpMyAdmin publicly accessible** — directory accessible without authentication; ChangeLog and README files exposed
- **Directory indexing enabled** on `/doc/`, `/icons/`, `/test/`, `/phpMyAdmin/`, `/twiki/`
- **phpinfo.php present** — exposes full server configuration to any visitor
- **PHP version 5.2.4** — end-of-life, no security patches
- **Apache 2.2.8** — end-of-life; latest at time of test was 2.4.54

---

## Red Team Operations — Active Exploitation

The following exploits were successfully executed during the penetration test phase.

### Exploit 1 — OpenSSH Brute Force (CVE-2016-6515)
**Tool:** Hydra  
**Vector:** Port 22 — OpenSSH authentication  
**Method:** Automated credential brute-force against SSH service  
**Result:** Valid credentials obtained; authenticated SSH session established on target  
**Business Impact:** Full command-line access to the server; lateral movement possible to other internal hosts

### Exploit 2 — Apache Slowloris DoS (CVE-2007-6750)
**Tool:** Metasploit (`auxiliary/dos/http/slowloris`)  
**Vector:** Port 80 — Apache HTTP Server 2.2.8  
**Method:** Partial HTTP requests sent continuously, exhausting Apache's connection pool  
**Result:** Web service rendered unavailable; denial of service confirmed  
**Business Impact:** Public-facing web services taken offline; availability of customer-facing systems compromised

### Exploit 3 — XSS Execution on Web Application
**Tool:** Burp Suite / Browser  
**Vector:** OWASP Juice Shop (via lowered security level after Slowloris access)  
**Method:** XSS payload injected into vulnerable input field  
**Result:** Script executed in browser context; session hijacking potential confirmed  
**Business Impact:** Attacker could steal session tokens, redirect users, or perform actions on behalf of authenticated users

### Exploit 4 — vsftpd Backdoor (CVE-2011-2523)
**Tool:** Metasploit  
**Vector:** Port 21 — vsftpd 2.3.4  
**Method:** Triggered the backdoor command sequence during FTP authentication  
**Result:** Root shell obtained on target machine  
**Business Impact:** Complete system compromise; attacker gains root access with no further privilege escalation required

### Exploit 5 — SMB / Port 445 Brute Force
**Tool:** Legion + Hydra  
**Vector:** Port 445 — SMB service  
**Method:** Automated brute force of login credentials via Legion scripting  
**Result:** Valid credentials obtained; Telnet session established using recovered credentials  
**Business Impact:** Authenticated access to internal network services; credential reuse risk across systems

---

## Blue Team — Detection & Monitoring

### Tools Used

| Tool | Purpose | Events Captured |
|------|---------|----------------|
| Kibana | Dashboard visualisation of SIEM logs | 9,115 total logs; 944 NIDS alerts; 803 classified alerts |
| OSSEC HIDS | Host-based intrusion detection | Detected port status changes; zero-packet events flagged |
| Squert | IDS event analysis and timeline visualisation | 533 "Listened ports status" events; VNC scan detected (ET SCAN 2002910) |
| Wireshark | Packet-level traffic analysis | TCP handshakes, ICMP floods, HTTP exploit traffic captured |
| Snort | Network-based threat detection | Custom rules written to alert on ICMP flooding and port scans |

### Detection Outcomes

| Attack Vector | Detected? | Response Quality |
|---------------|-----------|-----------------|
| Port scanning (Nmap / Legion) | ✅ Yes | Logged via Kibana; unusual traffic patterns identified |
| Slowloris DoS (Apache) | ✅ Partial | HTTP traffic flagged; no real-time alert triggered |
| FTP Exploit (vsftpd backdoor) | ⚠️ Partial | Abnormal connection patterns noted; no proactive block |
| MySQL attack | ❌ Missed | No alerts raised until post-compromise |
| Older CVEs (CVE-2002-1047, CVE-2006-5873) | ❌ Missed | Not immediately detected or blocked |

### Key Blue Team Findings

- **Detection was reactive, not proactive.** Manual log review in Kibana and Squert meant delayed identification of active exploits.
- **No automated alerting** was configured for high-severity exploit attempts — the team relied on periodic manual review.
- **Post-exploitation C2 traffic** was detected only after the fact, not in real-time.
- **Tool integration gap** — Kibana, Wireshark, and Squert operated in silos; no cross-correlation of alerts.

---

## Cybersecurity Risk Assessment — Red/Blue Team Summary

| Risk | Finding |
|------|---------|
| Unpatched/legacy services | Multiple end-of-life services (Apache 2.2.8, OpenSSH 4.7p1, PHP 5.2.4) actively running and exploitable |
| Lack of automated defences | No automated alerting or blocking — all detection manual |
| Misconfigured services | Anonymous FTP, phpMyAdmin exposed, TRACE method enabled, directory indexing active |
| Weak authentication | No 2FA on SSH or phpMyAdmin; weak passwords on FTP and MySQL brute-forced successfully |
| Attack surface | 23 open ports discovered on honeypot; Telnet and rpcbind identified as unnecessary exposure |

---

## Revised Risk Assessment (Post-Testing)

| Vulnerability | CVE | Impact | Revised Risk | Legislation |
|---------------|-----|--------|--------------|-------------|
| Lack of 2FA on SSH | CVE-2021-44790 | Unauthorised access to critical systems | **High** | Australian Privacy Act 1988 |
| Weak Password Policies | CVE-2022-29088 | Brute-force attacks → system compromise | **High** | Privacy Act 1988; Australian Cyber Security Strategy 2022 |
| Open Unnecessary Ports (Telnet, FTP) | CVE-2019-6111 | Exploitable attack surfaces | **Medium** | Australian Privacy Principles (APPs) |

---

## Remediation Recommendations

### Immediate Priority (Critical / High)

1. **Patch all end-of-life software** — Replace Apache 2.2.8, OpenSSH 4.7p1, vsftpd 2.3.4, and PHP 5.2.4 with current supported versions
2. **Implement MFA on all critical systems** — SSH, phpMyAdmin, and all admin interfaces enforced with Google Authenticator or equivalent *(2FA was enabled as part of this project in response to findings)*
3. **Enforce strong password policies** — Minimum complexity, expiry intervals, and lockout thresholds across Linux and Windows Server systems
4. **Disable unnecessary services** — Telnet (port 23), anonymous FTP, rpcbind (port 111) to reduce attack surface

### Medium Priority

5. **Deploy automated alerting** — Configure Splunk/Kibana alerting rules for critical events (exploit attempts, privilege escalation, unusual outbound traffic)
6. **Restrict phpMyAdmin access** — Remove public accessibility; require authentication and IP allowlisting
7. **Add missing HTTP security headers** — X-Frame-Options, X-Content-Type-Options, Content-Security-Policy
8. **Disable TRACE method** on Apache; remove phpinfo.php from production systems

### Ongoing

9. **Integrate SIEM tooling** — Cross-correlate Kibana, Wireshark, and Squert alerts for unified detection
10. **Conduct regular red team exercises** — Monthly penetration testing schedule to validate detection capability
11. **Implement IPS** in addition to IDS — Move from detect-only to detect-and-block posture

---

## Skills Demonstrated

| Domain | Evidence in This Project |
|--------|--------------------------|
| **Penetration Testing** | Exploited 5+ CVEs across FTP, SSH, HTTP, SMB, and web application vectors using Metasploit, Hydra, Burp Suite, and OWASP ZAP |
| **Vulnerability Assessment** | Nmap NSE, Nikto, DIRB scans; CVE identification and severity rating across 14 services |
| **Security Monitoring (SOC)** | Splunk, Kibana, OSSEC, Squert, Wireshark — log analysis, NIDS alerting, traffic classification |
| **GRC / Risk Management** | Initial and revised risk assessments; Australian legislative framework applied (Privacy Act, Criminal Code Act, Security of Critical Infrastructure Act); stakeholder feedback incorporated |
| **Network Architecture** | Designed and implemented 5-zone segmented virtual enterprise network with firewall, IDS, DMZ, and honeypot |
| **Incident Analysis** | Red/blue team gap analysis; detection latency identified; remediation roadmap produced |
| **Documentation** | Technical report, risk tables, network diagrams, implementation plan, and stakeholder communication produced throughout |

---

## Tools Reference

`Nmap` `Metasploit` `Hydra` `Burp Suite` `OWASP ZAP` `Nikto` `DIRB` `Legion` `Wireshark` `Splunk` `Kibana` `Squert` `OSSEC` `Snort` `Security Onion` `Kali Linux` `iptables` `VirtualBox`

---

*This project was completed as part of the ICT60220 Advanced Diploma of Information Technology (Cyber Security), conducted entirely within an isolated virtual lab environment.*
