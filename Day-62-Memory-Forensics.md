# Day 62 - Memory Forensics

## What It Is
Memory Forensics is the practice of capturing and analyzing the contents of a computer's RAM (Random Access Memory) to investigate security incidents, detect malware, and recover evidence that exists only in memory and never touches the disk. Many modern attack techniques — including fileless malware, injected code, and in-memory credential theft (Mimikatz, day 17) — deliberately avoid writing to disk to evade traditional antivirus and forensic tools. Memory forensics is often the only way to catch these attacks, recover encryption keys, find running malicious processes, and reconstruct what an attacker did on a system.

## How It Works
RAM is volatile — it loses its contents when the system is powered off. Memory forensics must be performed on a live system or from a memory dump captured before shutdown. A memory dump is a complete snapshot of everything in RAM at a specific moment — running processes, network connections, loaded DLLs, decrypted data, passwords, and more.

```
What memory forensics reveals:

Running Processes
All processes active at capture time including hidden ones
Rootkits (day 18) that hide from Task Manager are visible in raw memory
Process injection — malicious code injected into legitimate processes
(common technique: injecting into svchost.exe or explorer.exe)

Network Connections
All active and recently closed network connections
C2 connections from RATs (day 20) and Cobalt Strike beacons (day 27)
Connections that closed before the analyst started investigating

Loaded DLLs and Injected Code
Malicious DLLs loaded into legitimate processes
Reflective DLL injection — loading code without touching disk at all
Shellcode injected directly into process memory

Credentials and Encryption Keys
Plaintext passwords cached in memory by Windows LSASS process
(exactly what Mimikatz exploits — day 17)
Encryption keys for full-disk encryption — can decrypt drives
Browser saved passwords held in memory while browser is open
Session tokens and cookies from active sessions

Malware Artifacts
Unpacked malware — packed malware unpacks itself in memory to run
Config files embedded in malware — C2 addresses, encryption keys
Strings that reveal attacker infrastructure and tooling
```
