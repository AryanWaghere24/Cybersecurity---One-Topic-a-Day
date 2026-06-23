# Day 28 - SIEM & Log Analysis

## What It Is
A SIEM (Security Information and Event Management) is a platform that collects, aggregates, and analyzes log data from across an entire IT environment — servers, firewalls, endpoints, applications, cloud services — in one centralized place. Instead of a security analyst manually checking dozens of separate systems, a SIEM correlates events from everywhere and surfaces suspicious patterns that would be invisible looking at any single log source alone.

## How It Works
Every action on a network generates a log — a login, a file access, a network connection, a process execution. Individually most logs look harmless. A SIEM's value comes from correlation — connecting events across different sources to reveal an attack pattern.

```
Log Sources feeding into a SIEM:
- Firewall logs        - blocked/allowed connections
- Windows Event Logs   - logins, process creation, account changes
- Web server logs      - HTTP requests, status codes
- EDR/Antivirus logs   - malware detections, process behavior
- Cloud logs           - AWS CloudTrail, Azure Activity Logs
- Authentication logs  - VPN, Active Directory, SSO
```

Example correlation rule that would catch real attacks from this repo:
```
IF (failed login attempts > 50 from same IP within 5 minutes)   ← brute force
AND (successful login follows immediately after)                ← password cracked
AND (new process spawned: mimikatz.exe OR powershell -enc)       ← day 17 hash dumping
THEN trigger HIGH severity alert
```
