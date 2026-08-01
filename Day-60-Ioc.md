# Day 60 - IOC (Indicators of Compromise)

## What It Is
Indicators of Compromise (IOCs) are pieces of forensic evidence that suggest a system or network has been breached or is under attack. They are the digital fingerprints left behind by attackers — specific IP addresses, domain names, file hashes, registry keys, URLs, or behavioral patterns that indicate malicious activity. IOCs are the currency of threat intelligence — security teams collect them, share them, and use them to detect and respond to attacks. Finding a known malicious IP in your firewall logs or a known malware hash on an endpoint means you can immediately act rather than spending days investigating whether something suspicious is actually an attack.

## How It Works
IOCs exist at multiple levels — from simple network indicators to complex behavioral patterns. The pyramid of pain (a framework by David Bianco) describes IOCs by how difficult they are for attackers to change when defenders detect them.

```
Pyramid of Pain (bottom = easy for attacker to change, top = hard):

[TTPs]                    ← Hardest to change, most valuable
[Tools]
[Network/Host Artifacts]
[Domain Names]
[IP Addresses]
[Hash Values]             ← Easiest to change, least valuable

Hash Values (MD5, SHA1, SHA256)
File hashes of known malicious files
Easiest for attackers to change — recompile the malware, new hash
But easiest for defenders to check — run hash against VirusTotal

IP Addresses
Known C2 server IPs, attacker infrastructure
Attackers change IPs frequently — short-lived value
Still useful for blocking and detecting active campaigns

Domain Names
C2 domains, phishing domains, malware distribution sites
Harder to change than IPs — domain registration takes time
DGA (Domain Generation Algorithms) are attacker response to domain blocking

Network/Host Artifacts
Specific User-Agent strings, HTTP headers, registry keys
Mutex names created by malware, file paths used for persistence
More specific to the malware family — harder to change

Tools
Specific tools used: Cobalt Strike (day 27), Mimikatz (day 17)
Forcing attackers to switch tools is costly — significant pain
Tool signatures, beacon profiles, and JA3 hashes fall here

TTPs (Tactics Techniques and Procedures)
How attackers operate — their methodology and patterns
Mapped to MITRE ATT&CK (day 21)
Hardest to change — requires retraining the entire attack team
Most valuable intelligence for long-term defense
```
Common IOC types with examples:
```
File Hash:    d41d8cd98f00b204e9800998ecf8427e (MD5 of known malware)
IP Address:   185.220.101.45 (known Tor exit node / C2)
Domain:       malware-c2-domain.ru (known C2 domain)
URL:          http://evil.com/payload.exe (malware download URL)
Email:        phishing@spoofed-domain.com (phishing sender)
Registry Key: HKCU\Software\Microsoft\Windows\Run\malware (persistence)
Mutex:        Global\SuperMalwareMutex (malware instance check)
User-Agent:   python-requests/2.18.4 (unusual UA in web logs)
```
## Real-World Example
During the 2020 SolarWinds attack, once the initial compromise was discovered, security researchers rapidly extracted IOCs from the malware — specific domain names used for C2 (avsvmcloud.com), file hashes of the malicious DLL, and specific registry modifications used for persistence. These IOCs were shared through CISA advisories and threat intelligence platforms within days of discovery. Organizations that had integrated threat intelligence feeds could immediately query their logs for these IOCs — instantly knowing whether the SolarWinds backdoor had beaconed out from their environment without manually analyzing every system individually.

## Why It Matters
From an attacker's side, understanding IOCs helps in operational security — frequently rotating infrastructure, using living-off-the-land techniques to avoid tool-based IOCs, and mimicking legitimate traffic patterns to avoid behavioral IOCs. Nation-state actors specifically design their malware to avoid leaving obvious IOCs.

From a defender's side, IOCs are the foundation of threat detection at scale. A single analyst cannot manually review millions of log entries — but automated systems can instantly compare every log entry, file hash, and network connection against millions of known IOCs and alert on matches. Sharing IOCs through platforms like MISP and threat intelligence feeds multiplies their value — one organization's discovery becomes every organization's detection capability.

## Key Terms
- IOC (Indicator of Compromise): forensic evidence suggesting a system has been breached — file hashes, IPs, domains, behavioral patterns
- Pyramid of Pain: a framework ranking IOCs by how difficult they are for attackers to change when defenders detect them
- TTP (Tactics Techniques and Procedures): the highest-value IOC category describing how attackers operate, mapped to MITRE ATT&CK
- MISP (Malware Information Sharing Platform): an open source threat intelligence platform for sharing IOCs between organizations
- Threat Intelligence Feed: a continuously updated stream of IOCs from commercial or community sources integrated into security tools
