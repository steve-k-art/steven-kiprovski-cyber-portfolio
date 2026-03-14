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

![Nmap Scan](screenshots/t/nmap-scan.png)

**Findings:**  
- Identified active hosts within the 192.168.x.x range  
- Detected ICMP echo responses  
- Confirmed network accessibility and baseline topology  

---

## 🔍 2.2 ARP Scan

![ARP Scan](screenshots/t/arp-scan.png)

**Findings:**  
- Discovered local devices using ARP broadcast  
- Successfully resolved MAC addresses  
- Identified gateway and internal hosts  

---

## 🔍 2.3 DNS Enumeration (nslookup & dig)

![nslookup](screenshots/t/nslookup.png)  
![dig](screenshots/t/dig.png)

**Findings:**  
- No internal DNS records configured  
- NXDOMAIN responses indicate minimal DNS footprint  
- Useful for confirming lack of internal name resolution  

---

## 🔍 2.4 Traceroute

![Traceroute](screenshots/t/traceroute.png)

**Findings:**  
- Single hop to internal host  
- ICMP unreachable flags observed  
- Confirms flat network structure  

---

## 🔍 2.5 Service Enumeratio
