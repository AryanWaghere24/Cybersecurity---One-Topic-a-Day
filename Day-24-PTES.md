# Day 24 - PTES (Penetration Testing Execution Standard)

## What It Is
PTES (Penetration Testing Execution Standard) is a comprehensive framework that defines how a professional penetration test should be conducted from beginning to end. It covers everything — pre-engagement scoping, intelligence gathering, threat modeling, exploitation, post-exploitation, and final reporting. While MITRE ATT&CK (day 21) describes what attackers do and the Cyber Kill Chain (day 22) describes the attack flow, PTES tells a pentester how to professionally execute and document a security assessment.

## How It Works
PTES is divided into 7 phases that take a pentest from initial client conversation to final delivered report:

```
Phase 1 — Pre-Engagement Interactions
Define scope, rules of engagement, and legal authorization
Key documents: Statement of Work, NDA, Permission to Test letter
Critical: never touch anything outside the agreed scope

Phase 2 — Intelligence Gathering (Recon)
Collect as much information about the target as possible
OSINT: company structure, employees, technologies, IP ranges
Tools: Shodan, theHarvester, Maltego, LinkedIn, DNS enumeration

Phase 3 — Threat Modeling
Identify the most valuable assets and likely attack paths
Ask: what would a real attacker target and how would they get there?
Map findings from recon to potential attack vectors

Phase 4 — Vulnerability Analysis
Actively identify weaknesses in the target environment
Tools: Nessus, OpenVAS, Nmap, Nikto, Burp Suite
Combine automated scanning with manual testing

Phase 5 — Exploitation
Attempt to exploit identified vulnerabilities to gain access
Tools: Metasploit, custom exploits, manual techniques
All topics from Day 01-20 in this repo apply here

Phase 6 — Post Exploitation
Determine the real business impact of successful exploitation
Privilege escalation (day 08), lateral movement, data access
Demonstrate what a real attacker could achieve with that access

Phase 7 — Reporting
Document everything — findings, evidence, business impact, remediation
Two audiences: executive summary (non-technical) + technical report
Rating vulnerabilities by severity using CVSS scores
```
