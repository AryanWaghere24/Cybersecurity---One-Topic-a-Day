# Day 61 - Threat Actor Profiling (APT Groups)

## What It Is
Threat Actor Profiling is the process of identifying, tracking, and understanding the groups and individuals behind cyberattacks — their motivations, capabilities, preferred techniques, typical targets, and known infrastructure. APT (Advanced Persistent Threat) groups are the most sophisticated category of threat actors — typically nation-state sponsored or highly organized criminal organizations that conduct long-term, targeted campaigns against specific industries or governments. Understanding who is attacking you and why is the difference between reactive security (responding after every breach) and proactive security (anticipating and preparing for the specific threats most likely to target your organization).

## How It Works
Threat actors are tracked and named by security researchers using naming conventions that vary by vendor — each security company has its own naming system for the same groups.

```
Threat actor naming conventions:

CrowdStrike: Animal names by nation-state origin
- BEAR = Russia (Fancy Bear, Cozy Bear)
- PANDA = China (Deep Panda, Gothic Panda)
- CHOLLIMA = North Korea (Labyrinth Chollima)
- KITTEN = Iran (Charming Kitten, Phosphorus Kitten)

Microsoft: Chemical elements / weather themes
- Midnight Blizzard (formerly Nobelium) = Russia
- Volt Typhoon = China
- Lazarus = North Korea (also widely used name)

Mandiant/Google: APT numbering system
- APT28 = Fancy Bear (Russia, GRU)
- APT29 = Cozy Bear (Russia, SVR)
- APT41 = Double Dragon (China, dual espionage + cybercrime)
- APT38 = Lazarus subgroup (North Korea, financial theft)

Major APT groups and their characteristics:

APT28 / Fancy Bear (Russia - GRU military intelligence)
Targets: governments, military, elections, NATO countries
TTPs: spear phishing, credential theft, data exfiltration
Notable attacks: DNC hack 2016, World Anti-Doping Agency

APT29 / Cozy Bear (Russia - SVR foreign intelligence)
Targets: government, think tanks, healthcare, tech companies
TTPs: supply chain attacks, living off the land, long dwell time
Notable attacks: SolarWinds 2020, COVID vaccine research theft

Lazarus Group (North Korea - RGB)
Targets: banks, cryptocurrency exchanges, defense companies
TTPs: LinkedIn fake recruiters (day 49), watering hole, custom malware
Notable attacks: Sony Pictures 2014, Bangladesh Bank heist $81M, Bybit 2025

APT41 (China - MSS)
Targets: healthcare, telecom, technology, video games
TTPs: dual espionage and financial crime, supply chain compromise
Notable attacks: CCleaner supply chain 2017, multiple telecom providers
```

## Real-World Example
In 2022 Mandiant published a detailed profile of APT41 that revealed the group was simultaneously conducting state-sponsored espionage for Chinese intelligence while also running independent cybercrime operations for personal financial gain — stealing source code and sensitive data for the government while also operating ransomware and cryptocurrency theft schemes on the side. This dual-use characteristic is unique to APT41 and was only discoverable through years of tracking their infrastructure, malware families, and operational patterns. Organizations in APT41's target sectors (healthcare, gaming, telecom) could use this profile to specifically prepare for their known TTPs rather than defending against all possible attacks generically.

## Why It Matters
From an attacker's side (red teams), threat actor profiling informs adversary emulation — red teams specifically simulate the TTPs of the threat actors most likely to target their client's industry, making the exercise far more realistic and valuable than generic penetration testing.

From a defender's side, knowing which threat actors are most likely to target your organization based on your industry, geography, and data holdings allows you to prioritize defenses against their specific known techniques. A healthcare organization doesn't need to equally defend against all possible attacks — they need to specifically prepare for APT groups known to target healthcare. Mapping your detection coverage against the known TTPs of relevant threat actors (using MITRE ATT&CK, day 21) reveals exactly where your gaps are.

## Key Terms
- APT (Advanced Persistent Threat): a sophisticated, long-term targeted attack campaign typically conducted by nation-state actors or highly organized criminal groups
- Threat Actor: any individual, group, or nation-state conducting malicious cyber operations
- TTP (Tactics Techniques and Procedures): the characteristic methods a threat actor uses — their operational fingerprint mapped to MITRE ATT&CK
- Dwell Time: the length of time an attacker remains undetected inside a compromised network — APT groups often maintain access for months or years
- Adversary Emulation: red team exercises specifically simulating a known threat actor's TTPs rather than generic vulnerability testing

## One Tip / Tool

Tool: `MITRE ATT&CK Groups` database and `Mandiant Advantage` for threat actor intelligence

```
Free threat actor intelligence resources:

MITRE ATT&CK Groups:
https://attack.mitre.org/groups/
- Profiles of 130+ tracked threat actor groups
- Each group's known TTPs mapped to ATT&CK techniques
- Links to public reporting on each group

Mandiant/Google Threat Intelligence (free reports):
https://www.mandiant.com/resources/research
- Detailed APT group profiles and campaign reports
- Free annual M-Trends report with industry threat data

CISA Advisories:
https://www.cisa.gov/news-events/cybersecurity-advisories
- Government-issued alerts on specific threat actor campaigns
- Often includes IOCs (day 60) and TTPs for detected attacks

Recorded Future (free community):
https://www.recordedfuture.com/free
- Threat intelligence on active campaigns and actor tracking
