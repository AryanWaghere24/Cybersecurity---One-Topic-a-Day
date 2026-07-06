# Day 40 - Whaling

## What It Is
Whaling is a highly targeted spear phishing attack (day 39) specifically aimed at senior executives and high-value individuals — CEOs, CFOs, board members, legal counsel, and other C-suite targets. The name comes from "going after the big fish." Because executives have high-level access to sensitive systems, financial accounts, and confidential data, successfully phishing one of them can be catastrophically more damaging than targeting a regular employee. The attack is tailored to the executive's specific role, responsibilities, and the kinds of requests they regularly deal with.

## How It Works
Whaling attacks are more sophisticated and time-consuming than regular spear phishing because the target is high value and more security-aware. Attackers research the executive extensively before striking.

```
What makes whaling different from regular spear phishing:

Target profile research:
- Executive's name, title, direct reports, and board relationships
- Company financials, recent earnings calls, press releases
- Pending mergers, acquisitions, or major contracts
- Executive's travel schedule (often public or inferable)
- Personal details from LinkedIn, interviews, conference talks

Common whaling pretexts:
- Legal subpoenas ("You are required to appear regarding case #4821")
- Tax authority notices ("Urgent: IRS compliance required by Friday")
- Board-level requests ("Confidential: board resolution requires your signature")
- Merger/acquisition documents ("NDA attached for Project Falcon - do not forward")
- Urgent wire transfer requests from a "trusted partner" or "board member"
```
Attack flow:
```
1. Attacker researches target executive for days or weeks via OSINT
2. Crafts an extremely convincing email referencing real company events
3. Often impersonates lawyers, auditors, regulators, or other executives
4. Creates urgency and confidentiality ("do not discuss with colleagues")
5. Requests immediate action: wire transfer, credential entry, document signing
6. Uses legitimate-looking domains and professional language throughout
```

## Real-World Example
In 2016, Snapchat's payroll department received a whaling email impersonating CEO Evan Spiegel. The email requested employee payroll data — W-2 forms, salary information, and personal details for around 700 employees. The request was fulfilled before anyone verified it was legitimate. No systems were hacked, no malware was deployed. An email impersonating the CEO, sent to the right person, was enough to cause a significant data breach affecting hundreds of employees whose personal information was then exposed.

This same pattern — impersonating a CEO to request wire transfers or sensitive data — is so common it has its own name: CEO Fraud, a subset of Business Email Compromise (BEC, covered on day 43).

## Why It Matters
From an attacker's side, one successful whaling attack can yield significantly more value than dozens of regular phishing attacks — executives have access to financial systems, legal documents, M&A information, and can authorize large wire transfers that lower-level employees cannot.
