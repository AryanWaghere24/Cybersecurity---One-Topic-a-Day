# Day 22 - Cyber Kill Chain

## What It Is
The Cyber Kill Chain is a framework developed by Lockheed Martin in 2011 that describes the seven stages of a cyber attack — from initial reconnaissance all the way to the final objective. The idea comes from military targeting models — if you can disrupt any single link in the chain, you break the entire attack. It gives defenders a structured way to detect, respond to, and prevent attacks at each stage rather than just reacting after damage is done.


## How It Works
Every sophisticated cyber attack follows a predictable sequence of steps. The Kill Chain breaks this into 7 phases:

```
Phase 1 — Reconnaissance
Attacker gathers information about the target
Tools: OSINT, Shodan, LinkedIn scraping, DNS enumeration
Example: finding employee emails for phishing, scanning for open ports

Phase 2 — Weaponization
Attacker creates a malicious payload tailored to the target
Tools: msfvenom, macro-enabled Office documents, malicious PDFs
Example: building a RAT (day 20) disguised as an invoice PDF

Phase 3 — Delivery
Attacker delivers the weapon to the target
Methods: phishing email, malicious USB, watering hole attack
Example: sending the malicious PDF to HR via a spoofed email
