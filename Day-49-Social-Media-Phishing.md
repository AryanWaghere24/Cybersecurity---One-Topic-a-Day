# Day 49 - Social Media Phishing

## What It Is
Social Media Phishing is a category of phishing attacks conducted through social media platforms — Facebook, Instagram, LinkedIn, Twitter/X, TikTok, and others — where attackers create fake profiles, run malicious ads, send direct messages, or compromise real accounts to steal credentials, spread malware, or conduct financial fraud. Social media phishing is particularly effective because people are in a relaxed, social mindset when using these platforms, their guard is lower than when checking work email, and the platforms are designed to encourage clicking, sharing, and engaging with content from strangers.

## How It Works
Social media phishing takes multiple forms depending on the platform and the attacker's goal:

```
Common attack vectors:

Fake Profile Impersonation
Attacker creates a profile mimicking a real person or brand
Sends friend/connection requests to build a network
Then sends phishing links or requests money/information
Common on Facebook (fake friend) and LinkedIn (fake recruiter)

Malicious Ads
Paid social media ads promoting fake giveaways, investments, or products
"Elon Musk is giving away Bitcoin — click to claim yours"
Leads to credential harvesting or payment fraud pages
Extremely difficult to distinguish from legitimate sponsored content

Direct Message Phishing
Compromised accounts of real friends send messages:
"Hey! I found this photo of you — check it out [malicious link]"
Victim clicks because it appears to come from someone they know
Link either harvests credentials or installs malware

Fake Login Pages
"Your Instagram account will be deactivated — verify here"
Link goes to a convincing fake Instagram login page
Credentials stolen and used to compromise the real account

Fake Job Offers (LinkedIn specific)
Fake recruiter profiles with convincing work histories
Offer high-paying jobs requiring "skills assessment" downloads
Download is malware — North Korean Lazarus Group used this
extensively to target crypto and tech company employees
```

## Real-World Example
In 2020 the North Korean Lazarus Group conducted a sophisticated LinkedIn phishing campaign targeting employees of cryptocurrency companies. Fake recruiters with convincing LinkedIn profiles — complete with realistic work histories, endorsements, and connections — reached out to developers and security researchers with lucrative job offers. When targets expressed interest they were sent "skills assessment" documents that contained hidden malware. Once executed the malware provided backdoor access to the victim's machine — and through them, to their employer's systems and cryptocurrency holdings. Multiple cryptocurrency thefts worth hundreds of millions of dollars were linked to this LinkedIn phishing campaign.

## Why It Matters
From an attacker's side, social media provides enormous reach and targeting capability — attackers can identify specific job titles, companies, interests, and connections to craft highly relevant lures. Paid advertising tools designed for marketers work equally well for targeting phishing campaigns. Compromised accounts of real friends have near-perfect open and click rates.

From a defender's side, enabling MFA on all social media accounts is the most important technical control — a compromised password alone can't take over the account. Being skeptical of unsolicited DMs, job offers, and investment opportunities regardless of who appears to be sending them is essential. Verifying unusual messages from friends through a different channel (calling them) before clicking anything catches account compromise scenarios. Never download files sent through social media DMs regardless of the stated reason.
