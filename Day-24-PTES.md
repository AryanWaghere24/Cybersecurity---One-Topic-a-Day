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
## Real-World Example
A company hires a pentesting firm to assess their web application and internal network. The firm follows PTES — Phase 1 defines that only the company's public IP range and web app are in scope. Phase 2 reveals an employee's credentials in a data breach dump via OSINT. Phase 4 finds an outdated Apache server with a known CVE. Phase 5 exploits it to gain shell access. Phase 6 shows they could reach the internal database containing customer PII. Phase 7 delivers a report showing the entire attack chain with remediation steps. The company fixes the issues before a real attacker finds them — that's the entire value of a pentest.

## Why It Matters
From a pentester's side, PTES ensures nothing important gets skipped and that the engagement is conducted legally and professionally. The pre-engagement phase is especially critical — without written authorization, penetration testing is illegal regardless of intent.

From a defender's / client's side, PTES ensures the pentest they're paying for is thorough and covers all the right areas rather than just running an automated scanner. The final report gives a prioritized roadmap for fixing vulnerabilities based on real exploitability and business impact.

## Key Terms
- PTES: a standardized methodology for conducting professional penetration tests end to end
- Scope: the explicitly defined systems, IP ranges, and applications that are authorized for testing
- Rules of Engagement: agreed boundaries for how the test will be conducted — timing, methods allowed, escalation procedures
- CVSS (Common Vulnerability Scoring System): a standardized 0-10 scoring system for rating vulnerability severity
- Post Exploitation: the phase after gaining access where the pentester determines the real business impact of the compromise

## One Tip / Tool

Tool: `Obsidian` or `CherryTree` for pentest note taking, `Dradis` for collaborative reporting

```
Recommended pentest report structure:
1. Executive Summary (1-2 pages, non-technical, business impact focused)
2. Scope and Methodology
3. Findings Summary Table (vulnerability, severity, affected system)
4. Detailed Findings (each finding gets its own page):
   - Description
   - Evidence (screenshots, commands run)
   - Business Impact
   - CVSS Score
   - Remediation Steps
5. Appendices (raw tool output, scope confirmation)
```

A great free resource for learning PTES in practice is HackTheBox Pro Labs and TryHackMe — their lab environments are designed around realistic pentest scenarios that follow the PTES methodology from recon through reporting.
