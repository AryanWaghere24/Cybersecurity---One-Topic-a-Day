# Day 37 - What is Phishing?

## What It Is
Phishing is a type of social engineering attack where an attacker impersonates a trusted entity — a bank, a company, a colleague, or a government body — to trick victims into revealing sensitive information like passwords, credit card numbers, or personal data, or into taking a harmful action like clicking a malicious link or downloading malware. The name comes from "fishing" — casting a wide net and waiting for someone to take the bait. It's the single most common initial access vector in cyberattacks worldwide, responsible for over 90% of data breaches according to multiple industry reports.

## How It Works
Every phishing attack follows a basic structure regardless of the delivery method:

```
Step 1 — Reconnaissance
Attacker identifies the target (individual, organization, or broad population)
Gathers info: email addresses, company names, logos, employee names

Step 2 — Lure Creation
Crafts a convincing message impersonating a trusted entity
Uses urgency, fear, or authority to pressure quick action
Includes a malicious element: link, attachment, or request

Step 3 — Delivery
Sends the lure via email, SMS, phone call, social media, or other channel

Step 4 — Exploitation
Victim clicks the link → lands on a fake login page → credentials stolen
Victim opens attachment → malware executes on their machine
Victim follows instructions → transfers money or reveals sensitive info

Step 5 — Action on Objective
Attacker uses stolen credentials to access accounts
Deploys malware for persistence (day 18-20)
Moves laterally through the network (day 17)
```

Common phishing indicators:
```
- Sender email domain doesn't match the real organization
  (support@paypa1.com instead of support@paypal.com)
- Generic greeting ("Dear Customer" instead of your name)
- Urgent or threatening language ("Your account will be closed in 24 hours")
- Suspicious links (hover over reveals different URL than displayed)
- Unexpected attachments
- Requests for sensitive information via email
```

## Real-World Example
In 2016, John Podesta (Hillary Clinton's campaign chairman) fell victim to a phishing email disguised as a Google security alert asking him to change his password. A campaign aide incorrectly told him the email was "legitimate" when they meant to say "illegitimate." Podesta clicked the link, entered his credentials on a fake Google page, and handed over access to his entire Gmail account. The emails were subsequently leaked and became one of the most significant data breaches in US political history — all from one convincing phishing email.
