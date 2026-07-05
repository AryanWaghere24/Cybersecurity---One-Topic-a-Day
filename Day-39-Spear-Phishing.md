# Day 39 - Spear Phishing

## What It Is
Spear Phishing is a highly targeted form of phishing where the attacker customizes the attack specifically for one individual or a small group — using personal details, job role, recent activities, or relationships to make the message extremely convincing. Unlike regular email phishing (day 38) which casts a wide net with generic messages, spear phishing is a precision strike. The attacker invests significant time researching the target beforehand, making the resulting attack far more believable and far more likely to succeed.

## How It Works
The key difference from generic phishing is the research phase. Attackers use OSINT to gather personal details about the target before crafting the message.

```
Research sources attackers use:
- LinkedIn     - job title, company, colleagues, recent projects
- Twitter/X    - interests, recent activities, who they interact with
- Company website - team pages, org structure, email format
- News articles - recent company events, product launches
- Data breaches - previously leaked email/password combinations
- GitHub       - technologies used, project names, collaborators
```
Research sources attackers use:
- LinkedIn     - job title, company, colleagues, recent projects
- Twitter/X    - interests, recent activities, who they interact with
- Company website - team pages, org structure, email format
- News articles - recent company events, product launches
- Data breaches - previously leaked email/password combinations
- GitHub       - technologies used, project names, collaborators

Example of a generic phish vs spear phish:
```
Generic phish:
"Dear Customer, your account has been compromised. Click here to verify."

Spear phish targeting a finance employee:
"Hi Sarah, this is Mike from IT. I noticed your accounting software
threw an authentication error this morning. Given that you're
processing Q3 invoices this week, we need to revalidate your
credentials before 3pm today to avoid disruption.
Please use this link to re-authenticate: [malicious link]"
```
## Real-World Example
In 2011, RSA Security — one of the world's leading cybersecurity companies — was breached through a spear phishing email sent to a small group of employees. The email had the subject line "2011 Recruitment Plan" with an Excel attachment. One employee retrieved it from their spam folder and opened it — triggering a zero-day Flash exploit that installed a RAT (day 20) on their machine. Attackers then used that foothold to steal information about RSA's SecurID authentication tokens, compromising the security of millions of two-factor authentication deployments worldwide. A single targeted email with a believable subject line breached one of the most security-conscious organizations in the world.


