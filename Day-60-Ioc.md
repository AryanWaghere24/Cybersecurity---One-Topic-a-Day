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
