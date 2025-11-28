API Security Assessment -Summary Report

Assessment: Account Takeover | Weak Hashing | IDOR | Data Exposure

Author: Sreenath Thekkedan

Full report included in this folder 

API_Security_Assessment_Report

📌 Overview

This folder contains the API Security Assessment Report documenting real-world testing performed against a sample API.
The purpose of this assessment was to identify vulnerabilities related to:

Authentication & session security

Password hashing mechanisms

Authorization & access control

Sensitive data exposure

API error handling

Endpoint behaviour & response validation

The findings highlight multiple weaknesses that could lead to account takeover, data leakage, and compromised user privacy.

📝 Scope of Testing

The assessment focused on:

Login & credential handling

Token behaviour & identity switching

Hashing (MD5 weakness demonstration)

URL parameter tampering

IDOR (Insecure Direct Object Reference)

Excessive data exposure in responses

Broken link inspection

HTTP method handling and error responses

Out of Scope:

Backend source code

Infrastructure penetration testing

Social engineering

Denial of service

🚨 Key Findings (High-Level)

A detailed explanation with evidence is included in the full PDF report. Below is a summary:

1. Broken Authentication (High)

Credentials were processed via URL parameters instead of secure POST bodies.

Risk: Credentials exposed in logs, caches, browser history.

2. Sensitive Data Exposure (High)

API response returned email, token, and other sensitive fields in plaintext.

Risk: User impersonation.

3. Weak Hashing - MD5 (Critical)

Passwords hashed using MD5, which is easily reversible.

Risk: Password cracking & account compromise.

4. IDOR – Account Switching (High)

User identity was changeable by altering request parameters.

Risk: Full account takeover.

5. Broken Link Exposure (Medium)

External link scanning identified unused/legacy links (added for learning purposes).

6. Improper Error Handling (Medium)

API revealed internal behaviour using verbose error messages such as "Method Not Allowed".

📈 Severity Ratings

Critical: 1

High: 3

Medium: 2

Low: 0

🔧 Tools Used

Postman

MD5 Hash Generator

Browser-based link scanner

httpbin.org

📘 Full Documentation

The complete findings, screenshots, evidence, and recommendations are available in:

👉 API_Security_Assessment_Report.pdf
Located in this folder.

📌 Recommended Improvements (Summary)

Replace MD5 with secure hashing (bcrypt / Argon2 / scrypt)

Stop sending sensitive data in API responses

Enforce authorization checks for every user-owned object

Use POST bodies for credentials instead of URLs

Standardize error handling messages

Remove unused or broken links

📣 Author

Sreenath Thekkedan

Cybersecurity Analyst | Security Researcher


