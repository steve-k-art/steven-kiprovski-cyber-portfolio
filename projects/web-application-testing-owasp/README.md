# 🍊 Web Application Security Testing – OWASP Juice Shop  
*Testing modern web vulnerabilities in a deliberately insecure application*

---

## 📌 1. Project Overview

**Objective:**  
Identify and exploit common web application vulnerabilities in OWASP Juice Shop to demonstrate practical web security testing skills.

**Focus Areas:**  
- Authentication bypass  
- SQL injection  
- XSS  
- Sensitive data exposure  
- Broken access control  

**Tools Used:**  
`BurpSuite`, `ZAP`, `Hydra`, `Nmap`, `Browser DevTools`

---

# 🧪 2. Web Application Attacks

## 🔥 2.1 SQL Injection – Admin Login Bypass

![SQLi Login](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sql-login.png)

**Result:**  
- Successful authentication bypass  
- Full admin access obtained  

---

## 🧨 2.2 DOM‑Based XSS

![DOM XSS](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-dom-xss.png)

**Result:**  
- JavaScript executed in victim browser  
- Demonstrates client‑side injection risk  

---

## 🔐 2.3 CAPTCHA Bypass

![CAPTCHA Bypass](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-captcha-bypass.png)

**Result:**  
- CAPTCHA validation bypassed  
- No rate‑limiting or bot protection  

---

## 🕵️ 2.4 Sensitive Data Exposure

![Sensitive Data](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sensitive-data.png)

**Result:**  
- User data accessible without proper authorization  
- Demonstrates broken access control  

---

# ⚠️ 3. Key Findings

| ID | Vulnerability | Severity | Evidence |
|----|--------------|----------|----------|
| WA‑01 | SQL Injection | Critical | sqli-login |
| WA‑02 | DOM XSS | High | dom-xss |
| WA‑03 | CAPTCHA Bypass | High | captcha-bypass |
| WA‑04 | Sensitive Data Exposure | High | sensitive-data |
| WA‑05 | Weak Authentication | Medium | login tests |

---

# 🛠️ 4. Recommendations

### 🔐 Authentication  
- Implement prepared statements  
- Enforce strong password policies  
- Add rate‑limiting and CAPTCHA validation  

### 🧱 Input Validation  
- Sanitize all user input  
- Implement server‑side validation  
- Use Content Security Policy (CSP)  

### 🕵️ Access Control  
- Enforce RBAC  
- Validate authorization on every request  
- Protect sensitive endpoints  

---

# 🏁 5. Conclusion
The OWASP Juice Shop assessment demonstrated multiple high‑risk vulnerabilities including SQL injection, XSS, and authentication bypass. These findings highlight the importance of secure coding practices, proper input validation, and robust access control mechanisms.

---

# 📚 6. Appendix

![SQLi Login](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sql-login.png)

![DOM XSS](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-dom-xss.png)

![CAPTCHA Bypass](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-captcha-bypass.png)

![Sensitive Data](https://raw.githubusercontent.com/steve-k-art/steven-kiprovski-cyber-portfolio/main/screenshots%202/juice-sensitive-data.png)
