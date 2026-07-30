# Day 59 - Dark Web Monitoring

## What It Is
Dark Web Monitoring is the practice of continuously scanning dark web forums, marketplaces, and data dump sites for an organization's stolen credentials, sensitive data, intellectual property, or mentions of planned attacks. The dark web is a part of the internet accessible only through specialized software like Tor — it hosts both legitimate privacy-focused communities and criminal marketplaces where stolen data, credentials, malware, and hacking services are bought and sold. For defenders, monitoring this ecosystem provides early warning of breaches, credential exposures, and emerging threats before they're actively exploited.

## How It Works
The dark web isn't indexed by regular search engines and can't be accessed through a standard browser. Accessing it requires the Tor network, which anonymizes traffic by routing it through multiple encrypted relays.

```
Dark web ecosystem relevant to cybersecurity:

Data Breach Markets
Stolen credentials, credit cards, and personal data sold in bulk
Examples: forums where breach databases are posted and traded
A defender monitoring these can discover their organization's
credentials were stolen before attackers use them for initial access

Ransomware Leak Sites
Most major ransomware groups maintain dark web sites
They publish stolen data from victims who refuse to pay
Defenders monitor these to detect if their organization is listed
Early detection gives time to respond before public disclosure

Hacking Forums
Discussions of new vulnerabilities, tools, and attack techniques
Sometimes specific organizations are mentioned as targets
Threat intelligence teams monitor for mentions of their brand

Initial Access Brokers
Criminals who specialize in breaking into organizations
Then sell that access to ransomware groups or other attackers
Monitoring for your organization being sold as "access available"
provides critical early warning of an imminent ransomware attack

Paste Sites & Code Repositories
Stolen data often posted to Pastebin, PrivateBin, and similar sites
Credentials, internal documents, and source code dumped publicly
Automated monitoring catches these within minutes of posting
```

Accessing the dark web safely for research:
```bash
# Tor Browser - the standard way to access .onion sites
# Download from: https://www.torproject.org/download/

# For programmatic access in a research context
# Use stem library to control Tor from Python
pip install stem requests[socks]

import requests
proxies = {
    'http': 'socks5h://127.0.0.1:9050',
    'https': 'socks5h://127.0.0.1:9050'
}
# Route requests through Tor
response = requests.get('http://example.onion', proxies=proxies)

# IMPORTANT: Only access sites you're authorized to research
# Many dark web sites host illegal content — stay within legal boundaries
```

## Real-World Example
In 2021 the credentials of over 500 million LinkedIn users appeared on a dark web forum — scraped from LinkedIn's public data but compiled into a searchable database being sold for cryptocurrency. Organizations with dark web monitoring in place received alerts within hours of the data appearing, allowing them to proactively notify affected employees and enforce password resets before attackers could use the credentials for credential stuffing attacks (trying leaked passwords across other services). Without dark web monitoring, many organizations only discovered their employees' credentials were exposed when accounts started being compromised weeks later.

## Why It Matters
From an attacker's side, the dark web provides a marketplace for everything needed to conduct attacks — stolen credentials for initial access, exploit kits, malware-as-a-service, and even targeted attack services against specific organizations. Understanding this ecosystem helps defenders anticipate what attackers have access to.

From a defender's side, dark web monitoring provides the earliest possible warning of credential exposure and data breaches — often before the organization itself knows they've been compromised. The average time between a breach occurring and an organization discovering it independently is measured in months. Dark web monitoring can compress that to hours, dramatically reducing the window attackers have to exploit stolen data before defenders respond.

## Key Terms
- Dark Web: the portion of the internet accessible only through anonymizing networks like Tor, hosting both privacy-focused and criminal content
- Tor (The Onion Router): a network that anonymizes internet traffic by routing it through multiple encrypted relays, used to access .onion sites
- Initial Access Broker: a cybercriminal who specializes in breaking into organizations and selling that access to other attackers
- Credential Stuffing: using leaked username/password combinations to attempt login across multiple services, exploiting password reuse
- Ransomware Leak Site: a dark web site maintained by ransomware groups to publish stolen data from victims who refuse to pay ransom

## One Tip / Tool

Tool: `HaveIBeenPwned API` for credential monitoring and `SpiderFoot` for automated dark web and OSINT monitoring

```bash
# HaveIBeenPwned - check if email/domain appears in known breaches
# Free API for personal use, paid for bulk organizational monitoring
curl "https://haveibeenpwned.com/api/v3/breachedaccount/test@example.com" \
  -H "hibp-api-key: YOUR_API_KEY"

# check all breaches for a domain (shows all employee emails exposed)
curl "https://haveibeenpwned.com/api/v3/breacheddomain/yourcompany.com" \
  -H "hibp-api-key: YOUR_API_KEY"

# SpiderFoot - automated OSINT and dark web monitoring
pip install spiderfoot
sf -l 127.0.0.1:5001  # launch web interface
# includes modules for dark web paste site monitoring
# breach database checking, and credential exposure detection

# Commercial dark web monitoring services (most mature option):
# - Recorded Future
# - Digital Shadows
# - Flare (formerly Flare Systems)
# These provide continuous monitoring with analyst context
# most enterprises use these rather than building their own capability
```

Dark web monitoring is most valuable as a continuous, automated capability rather than a one-time check. Credentials appear on dark web forums continuously — from ongoing breaches, old breach databases being re-shared, and newly compiled combo lists. Setting up automated monitoring with alerting means your security team learns about exposures in near real time rather than discovering them during an incident investigation after accounts have already been compromised.
