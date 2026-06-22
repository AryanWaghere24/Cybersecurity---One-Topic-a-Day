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
