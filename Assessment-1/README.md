API Security Assessment – Missing Security Headers & Token Exposure
Self-Driven API Penetration Test | Learning Project

📌 Overview
This folder contains the results of a hands-on API security assessment performed as part of an ongoing cybersecurity learning initiative.
 The objective was to explore real-world API weaknesses and understand how insecure configurations can lead to authentication bypass, information leakage, and brute-force attack opportunities.
The full PDF report documents all findings with screenshots, detailed explanations, and proof-of-concept examples.

🎯 Scope of Assessment
The testing covered the following areas:
API authentication workflow (GET vs POST)


Server header information leakage


Sensitive data exposure in API responses


Security headers (CSP, HSTS, MIME protections)


Username enumeration behaviour


Rate limiting & brute-force resistance


Response analysis & token exposure


No backend code or infrastructure testing was performed.

⚠️ Key Findings (Summary)
1. Insecure Authentication Method - Credentials in URL
The API accepted login credentials using a GET request, exposing username & password in the URL.
 As explained on page 1, this exposes sensitive data through:
Browser history


Server logs


Referrer headers


Network monitoring


Secure design: use POST + TLS for credential exchange.

2. Server Version Disclosure - Information Leakage
The server returned Apache/2.4.18 (Ubuntu) in the response headers (page 2).
 This enables attackers to identify:
OS version


Web server version


Associated CVEs for targeted exploits


This should be suppressed wherever possible.

3. Sensitive Data Exposure in API Response
The API returned:
Username


Email ID


Authentication Token


As shown on page 3, this is a major exposure risk and may enable account takeover if intercepted or replayed.

4. Missing Essential Security Headers
As analysed on page 3-4, the API lacked headers such as:
Content Security Policy (CSP)


HTTP Strict Transport Security (HSTS)


X-Frame-Options


X-Content-Type-Options


Without these, the application is vulnerable to:
XSS attacks


Clickjacking


MITM downgrade attacks


Token leakage



5. Username Enumeration
The system returned different messages for invalid usernames vs wrong passwords (page 5).
 Although the specific test passed, the behaviour could still aid attackers.

6. No Rate Limiting - Brute Force Exposure
As demonstrated with Burp Suite screenshots on pages 6-7, the login endpoint allowed unlimited attempts.
 Burp Intruder successfully revealed correct characters based on:
Response size changes


Status code variations


This makes brute-force attacks practical.

🛠️ Tools Used
Postman


Burp Suite Intruder


Browser response inspector


Manual endpoint tampering



📘 Full Documentation
The complete detailed findings, screenshots, and analysis are provided in:
📄 API Security Testing - Missing Security Headers & Token Exposure.pdf

🔧 Recommendations (High-Level)
Enforce POST over GET for authentication


Remove server version disclosures


Stop returning sensitive data in plaintext


Add CSP, HSTS, and other hardening headers


Implement uniform error messages


Add rate limiting & lockout policies


Implement monitoring for suspicious login patterns



👤 Author
Sreenath Thekkedan
 Cybersecurity Analyst | Security Researcher
