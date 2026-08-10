# Day 63 - Disk Forensics

## What It Is

Disk Forensics is the practice of acquiring and analyzing the contents of storage devices — hard drives, SSDs, USB drives, and memory cards — to investigate security incidents, recover deleted evidence, and reconstruct attacker activity. While memory forensics (day 62) captures volatile data that disappears on reboot, disk forensics examines persistent storage that survives power cycles. Attackers leave traces on disk even when they try to clean up — deleted files, modified timestamps, registry entries, log fragments, and filesystem metadata all tell the story of what happened on a system and when.

## How It Works
Disk forensics starts with creating a forensic image — a bit-for-bit copy of the entire storage device including deleted files, unallocated space, and filesystem metadata. Analysis is always performed on the image, never the original, to preserve evidence integrity.

```
Disk forensics workflow:

Step 1 — Forensic Acquisition
Create a verified bit-for-bit image of the storage device
Hash the original and image to prove integrity (MD5/SHA256)
Never work directly on original evidence

Step 2 — File System Analysis
Examine file system structure for artifacts:
- File creation, modification, access timestamps (MACE times)
- Recently deleted files in unallocated space
- Hidden files and alternate data streams (NTFS ADS)
- Recycle Bin contents
- File system journal/logs (NTFS $MFT, $LogFile, $UsnJrnl)

Step 3 — Registry Analysis (Windows)
Windows Registry stores massive amounts of forensic evidence:
- Recently accessed files (RecentDocs, OpenSaveMRU)
- Programs that ran (UserAssist, AppCompatCache, Prefetch)
- USB devices ever connected (USBSTOR)
- Network connections (NetworkList)
- Persistence mechanisms (Run keys — day 18 rootkits use these)
- User account activity and login times

Step 4 — Artifact Recovery
Browser history, downloads, cached pages
Email client data
Windows Event Logs (login events, process creation, network)
Prefetch files — evidence of program execution even if deleted
LNK files — shortcut files revealing recently opened documents

Step 5 — Timeline Analysis
Correlate all timestamps across file system, registry, and logs
Build a chronological timeline of attacker activity
Identify the initial access point and subsequent actions
```

Key forensic artifacts and what they reveal:
```
Windows Prefetch (.pf files)
Location: C:\Windows\Prefetch\
Reveals: every program that executed on the system
Even if malware deleted itself, prefetch proves it ran
Contains: program name, run count, last run time, files accessed

Windows Event Logs
Location: C:\Windows\System32\winevt\Logs\
Key events:
4624 - Successful login
4625 - Failed login (brute force detection)
4648 - Explicit credential login (Pass the Hash indicator, day 17)
4688 - Process creation (what commands were run)
7045 - New service installed (persistence indicator)
