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
