# Day 64 - Log Forensics

## What It Is
Log Forensics is the practice of collecting, preserving, and analyzing log data from systems, applications, and network devices to reconstruct security incidents, detect attacker activity, and establish a timeline of events. Logs are the most widely available source of forensic evidence in any environment — every operating system, web server, firewall, authentication system, and cloud service generates them continuously. While memory forensics (day 62) captures volatile evidence and disk forensics (day 63) examines persistent storage, log forensics focuses specifically on the recorded audit trail that systems generate about their own activity.

## How It Works
Logs record events in structured or semi-structured formats with timestamps, event types, and contextual details. The challenge isn't collecting logs — it's knowing which logs matter, where to find them, and how to correlate events across multiple sources to reconstruct an attack.

```
Critical log sources for forensic investigation:

Windows Event Logs
Location: C:\Windows\System32\winevt\Logs\
Key log files:
- Security.evtx   : authentication, privilege use, account changes
- System.evtx     : system events, service installs, driver loads
- Application.evtx: application crashes, errors, warnings

Critical Windows Event IDs:
4624  Successful logon (note logon type: 3=network, 10=remote interactive)
4625  Failed logon (repeated = brute force attempt)
4648  Logon with explicit credentials (Pass the Hash indicator, day 17)
4672  Special privileges assigned (admin logon)
4688  Process creation (what programs ran and who ran them)
4698  Scheduled task created (persistence mechanism, day 18-20)
4720  User account created (attacker creating backdoor accounts)
4776  Credential validation (NTLM authentication attempts)
7045  New service installed (common persistence and rootkit indicator)

Linux Logs
/var/log/auth.log     : SSH logins, sudo usage, authentication
/var/log/syslog       : general system events
/var/log/apache2/     : web server access and error logs
/var/log/secure       : authentication on RHEL/CentOS systems
~/.bash_history       : command history (often cleared by attackers)
/var/log/cron         : scheduled task execution
