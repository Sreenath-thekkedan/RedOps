API Security Assessment - Missing Security Headers & Token Exposure

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
   This exposes sensitive data through:

   Browser history

  Server logs

  Referrer headers

  Network monitoring

  Secure design: Use POST + TLS for credential exchange.

2. Server Version Disclosure - Information Leakage

  The server returned Apache/2.4.18 (Ubuntu) in the response headers.
  This reveals:

  OS version

  Web server version

  Known CVEs

  This should be suppressed.

3. Sensitive Data Exposure in API Response

  The API returned:

  Username

  Email ID

  Authentication Token

  This increases risk of account takeover if intercepted.

4. Missing Essential Security Headers

  The API lacked:

  Content Security Policy (CSP)

  HTTP Strict Transport Security (HSTS)

  X-Frame-Options

  X-Content-Type-Options

  This increases risk of:

  XSS

  Clickjacking

  MITM attacks

  Token leakage

5. Username Enumeration

  Different error messages are shown for invalid usernames vs wrong passwords.
  This behaviour can help attackers identify valid accounts.

6. No Rate Limiting - Brute Force Exposure

  Burp Suite Intruder demonstrated unlimited login attempts.
  Correct characters were revealed based on:

  Response size differences

Status code changes

  This enables brute-force attacks.

🛠️ Tools Used

  Postman

  Burp Suite Intruder

  Browser response inspector

  Manual endpoint tampering

📘 Full Documentation

  📄 API Security Testing - Missing Security Headers & Token Exposure.pdf

🔧 Recommendations (High-Level)

   Enforce POST over GET for authentication

   Remove server version disclosures

   Stop returning sensitive data in plaintext

   Add CSP, HSTS, and other headers

   Use uniform error messages

   Add rate limiting & lockout policies

   Implement monitoring for login abuse

👤 Author

  Sreenath Thekkedan

  Cybersecurity Analyst | Security Researcher
