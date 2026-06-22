# Day 27 - Cobalt Strike (Concepts)

## What It Is
Cobalt Strike is a commercial adversary simulation platform designed for professional red teams to emulate the full lifecycle of a sophisticated, stealthy attacker over a long engagement. Unlike Metasploit (day 25) which focuses on individual exploitation, Cobalt Strike focuses on what happens after access is gained — covert command and control, lateral movement, and long-term persistence that mimics how real advanced threat actors operate inside a network for weeks or months.

## How It Works
Cobalt Strike's core component is the Beacon — its signature payload, conceptually similar to a RAT (day 20) but built specifically for stealth and flexibility in enterprise environments.

```
Team Server  - the C2 server red teamers control, manages all active Beacons
Beacon       - the payload running on compromised machines, checks in periodically
Listener     - defines how Beacons communicate back (HTTP, HTTPS, DNS, SMB)
Malleable C2 - profile system that disguises Beacon traffic to look like legitimate web traffic
```

Key concepts that make Cobalt Strike distinct:

```
Sleep Time / Jitter
Beacons don't maintain constant connections - they "sleep" and check in periodically
This avoids the kind of constant outbound traffic that's easy to detect
A beacon might check in every 60 seconds with random jitter to avoid predictable patterns

Malleable C2 Profiles
Disguises Beacon traffic to look like normal traffic to services like Google, AWS, or Slack
Makes network detection significantly harder than a typical reverse shell (day 09)

Pivoting
Once inside one machine, Beacon can pivot to reach internal-only systems
Similar concept to lateral movement covered in pass the hash (day 17)

Peer-to-Peer C2
Beacons can relay through each other (SMB pivoting) so only one machine
needs direct internet access, reducing the network footprint significantly
```

## Real-World Example
Cobalt Strike is legitimately licensed for red teams, but cracked/leaked versions have become the single most common post-exploitation tool used in real ransomware attacks. Groups behind Ryuk, Conti, and many other major ransomware operations used cracked Cobalt Strike Beacons for lateral movement and persistence before deploying ransomware. The 2021 Conti ransomware playbook leak revealed operators using Cobalt Strike extensively to map networks, escalate privileges, and stage data theft before final encryption — essentially using a legitimate red team tool as their primary attack infrastructure.

## Why It Matters
From a red team's side, Cobalt Strike enables realistic adversary simulation that tests an organization's detection capabilities against techniques actual sophisticated attackers use — not just running known exploits but operating with stealth over extended periods.

From a defender's side, Cobalt Strike's prevalence in real attacks means security teams specifically train detection systems to spot Beacon traffic patterns — unusual jitter-based check-ins, Malleable C2 profile signatures, and known JA3/JARM TLS fingerprints associated with cracked Cobalt Strike servers. Many EDR vendors now have dedicated Cobalt Strike detection signatures because it's so commonly abused.

## Key Terms
- Beacon: Cobalt Strike's primary payload, a stealthy persistent agent on the compromised host
- Team Server: the central C2 server that red team operators use to manage all active Beacons
- Malleable C2: configuration profiles that disguise C2 traffic to mimic legitimate web services
- Jitter: randomized variation in Beacon check-in timing to avoid predictable network patterns
- Adversary Simulation: red team exercises designed to mimic real-world advanced threat actor behavior rather than just testing for known vulnerabilities
