# 🔍 Stage 0 – Penetration Test  
**PDF Pages:** 5–13  
**Screenshots Folder:** `/screenshots/stage0/`

This stage focuses on identifying vulnerabilities, analysing CVEs, and assessing DataTrust’s risk exposure.

---

## 📘 0.1 Risk Appetite Summary  
**PDF Page:** 5

![Risk Appetite Summary](screenshots/stage0/risk-appetite-summary.png)

DataTrust demonstrates a **moderate risk appetite**, with low tolerance for vulnerabilities affecting sensitive data such as PII and ePHI.

---

## 🔥 0.2 Identified Vulnerabilities & CVEs

### EternalBlue – SMBv1 Remote Code Execution  
**CVE:** CVE‑2017‑0144  
**PDF Page:** 6  

![EternalBlue Evidence](screenshots/stage0/eternalblue-cve-2017-0144.png)

---

### HSTS Not Enforced  
**CVE:** CVE‑2014‑3566 (POODLE)  
**PDF Page:** 7  

![HSTS Misconfiguration](screenshots/stage0/hsts-misconfiguration.png)

---

### Cookie Missing HttpOnly  
**PDF Page:** 7  

![Cookie Missing HttpOnly](screenshots/stage0/cookie-missing-httponly.png)

---

### Apache HTTPD MITM  
**CVE:** CVE‑2016‑4975  
**PDF Page:** 7  

![Apache MITM](screenshots/stage0/apache-mitm-cve-2016-4975.png)

---

### Unpatched Legacy Services  
**ProFTPD – CVE‑2015‑3306**  
**OpenSSH – CVE‑2016‑6515**  
**PDF Page:** 8  

![ProFTPD CVE](screenshots/stage0/proftpd-cve-2015-3306.png)  
![OpenSSH CVE](screenshots/stage0/openssh-cve-2016-6515.png)

---

### SChannel Vulnerability  
**CVE:** CVE‑2014‑6321  
**PDF Page:** 9  

![SChannel CVE](screenshots/stage0/schannel-cve-2014-6321.png)

---

## 📊 0.3 Initial Risk Assessment Table  
**PDF Pages:** 10–11  

![Initial Risk Assessment](screenshots/stage0/initial-risk-assessment-table.png)

---
