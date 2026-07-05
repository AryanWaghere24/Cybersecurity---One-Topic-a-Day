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
`````
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

## Why It Matters
From an attacker's side, spear phishing has dramatically higher success rates than generic phishing because personalization removes most of the obvious red flags victims are trained to look for. Nation-state threat actors almost exclusively use spear phishing for initial access because it's reliable, deniable, and difficult to attribute.

From a defender's side, technical controls like SPF/DKIM/DMARC (day 38) help but don't fully stop spear phishing since attackers often use legitimate email services or properly registered lookalike domains. The most effective defenses are security awareness training, verifying unusual requests through a separate communication channel, and limiting publicly available personal and organizational information — reducing the OSINT attackers can gather during research.

## Key Terms
- Spear Phishing: a targeted phishing attack personalized using researched details about a specific individual or organization
- OSINT (Open Source Intelligence): gathering information about a target from publicly available sources before an attack
- Pretexting: creating a believable fabricated scenario tailored to the target to make the request seem legitimate
- Zero-day: a vulnerability unknown to the software vendor with no available patch at the time of exploitation
- Whaling: a specific type of spear phishing targeting senior executives (day 40)

## One Tip / Tool

Tool: `theHarvester` for understanding what OSINT an attacker can gather about your organization

```bash
# theHarvester - gather emails, subdomains, and names from public sources
theHarvester -d targetcompany.com -b google,linkedin,twitter

# this shows exactly what an attacker sees during their research phase
# use it on your own organization to identify what's publicly exposed
# then reduce that exposure before attackers use it against you
```

The best personal defense against spear phishing — Google yourself and your organization regularly. See what an attacker would find during their OSINT phase. If your LinkedIn shows your current projects, your manager's name, and your company's email format, an attacker has everything they need to craft a convincing spear phish targeting you specifically.
