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

$MFT (Master File Table)
NTFS metadata for every file ever created on the volume
Even deleted files leave MFT entries
Reveals: exact timestamps, file sizes, file paths

Browser Artifacts
Chrome: C:\Users\[user]\AppData\Local\Google\Chrome\User Data\Default\
- History (SQLite database)
- Downloads
- Cookies and cached login sessions
```

## Real-World Example
In the 2013 Target breach investigation (referenced in day 22), disk forensics on compromised point-of-sale systems revealed the exact malware used (BlackPOS), when it was installed, which systems it spread to, and the specific data exfiltration mechanism — all reconstructed from disk artifacts even after the attackers had attempted to remove traces of their activity. Prefetch files proved the malware had executed even after the executable was deleted. Windows Event Logs showed the exact account used for lateral movement. Registry Run keys revealed the persistence mechanism. The complete attack timeline was reconstructed from disk artifacts alone, providing the evidence needed for attribution and legal proceedings.

## Why It Matters
From an attacker's side, anti-forensics techniques attempt to defeat disk forensics — timestomping (modifying file timestamps to mislead investigators), secure deletion tools, encryption, and living-off-the-land techniques that use built-in system tools leaving fewer unusual artifacts. But even sophisticated attackers almost always leave some disk traces.

From a defender's side, disk forensics provides the persistent evidence layer that memory forensics can't — even after a system is rebooted and memory is lost, disk artifacts survive. Enabling Windows audit policies (process creation logging, logon events) maximizes the forensic value of event logs. Collecting forensic images immediately after detecting a compromise, before systems are wiped and rebuilt, is critical for preserving evidence for investigation and potential legal action.

## Key Terms
- Disk Forensics: acquiring and analyzing storage device contents to investigate security incidents and recover evidence
- Forensic Image: a verified bit-for-bit copy of a storage device used for analysis while preserving the original evidence
- MACE Times: the four timestamps associated with files — Modified, Accessed, Changed (metadata), Entry Modified — used to reconstruct timelines
- Prefetch: Windows files recording program execution history — forensic evidence that a program ran even if it was subsequently deleted
- Anti-Forensics: techniques used by attackers to destroy, hide, or alter digital evidence to impede forensic investigation

## One Tip / Tool

Tool: `Autopsy` (free, open source) and `FTK Imager` (free acquisition tool) — the standard beginner disk forensics toolkit


```bash
# FTK Imager - acquire a forensic image (Windows GUI tool)
# Download from: https://www.exterro.com/ftk-imager
# Creates verified forensic images with MD5/SHA1 hashes
# Can also mount images for read-only examination

# Autopsy - open source forensic analysis platform
# Download from: https://www.autopsy.com/download/
# Analyzes disk images for:
# - Deleted file recovery
# - Web artifacts (browser history, downloads)
# - Email analysis
# - Registry analysis
# - Timeline generation
# - Keyword search across entire image

# Command line tools for Linux-based forensics:

# Create a forensic image with dd
dd if=/dev/sda of=/evidence/disk.img bs=4M status=progress

# Verify image integrity
md5sum /dev/sda > original.md5
md5sum /evidence/disk.img > image.md5
diff original.md5 image.md5  # should be identical

# Mount image read-only for examination
mount -o ro,loop /evidence/disk.img /mnt/evidence

# Recover deleted files
foremost -i /evidence/disk.img -o /evidence/recovered/

# Extract Windows prefetch files and parse them
python3 -m pip install libscca-python
# or use PECmd from Eric Zimmerman's tools (Windows)
```

Practice disk forensics on **Digital Forensics CTF challenges** from platforms like CyberDefenders (cyberdefenders.org) and BlueTeamLabs Online (blueteamlabs.online) — both provide realistic disk images from simulated incidents with guided investigation questions, making them ideal for building practical disk forensics skills.
