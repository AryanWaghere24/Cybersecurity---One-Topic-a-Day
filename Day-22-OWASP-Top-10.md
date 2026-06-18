# Day 23 - OWASP Top 10

## What It Is
The OWASP Top 10 is a standard awareness document published by the Open Worldwide Application Security Project that lists the 10 most critical security risks to web applications. It's updated every few years based on real-world data from hundreds of organizations and thousands of applications. It's not a complete list of every vulnerability — it's a prioritized ranking of what matters most, used as a baseline by developers, auditors, and security teams worldwide.

## How It Works
The current OWASP Top 10 (2021 edition) categories are:

```
A01 — Broken Access Control
Users can act outside their intended permissions
Example: changing a URL parameter to view another user's data

A02 — Cryptographic Failures
Sensitive data exposed due to weak or missing encryption
Example: storing passwords in plaintext or weak MD5 hashes (day 15)

A03 — Injection
Untrusted data sent to an interpreter as part of a command or query
Example: SQL Injection (day 04), Command Injection, XSS (day 05)

A04 — Insecure Design
Missing or ineffective security controls baked into the design itself
Example: no rate limiting on a login form, allowing brute force

A05 — Security Misconfiguration
Insecure default configs, open cloud storage, verbose error messages
Example: exposed admin panels, default credentials left unchanged

A06 — Vulnerable and Outdated Components
Using libraries or frameworks with known vulnerabilities
Example: an old version of a CMS plugin with a public CVE

A07 — Identification and Authentication Failures
Weak login mechanisms allowing credential stuffing or session hijacking
Example: no account lockout, predictable session tokens

A08 — Software and Data Integrity Failures
Trusting code or data without verifying its integrity
Example: unsigned software updates, insecure deserialization

A09 — Security Logging and Monitoring Failures
Insufficient logging means breaches go undetected for long periods
Example: no alerts on repeated failed login attempts

A10 — Server-Side Request Forgery (SSRF)
Tricking a server into making unintended requests (day 07)
Example: the Capital One breach via AWS metadata SSRF
```
