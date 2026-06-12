# Day 18 - Rootkits

## What It Is
A Rootkit is a collection of malicious software designed to gain persistent root or admin level access to a system while actively hiding its presence from the operating system, security tools, and the user. The name comes from "root" (the highest privilege on Unix systems) and "kit" (a set of tools). Unlike regular malware that just runs and does damage, a rootkit's primary goal is to stay hidden as long as possible while maintaining access.

## How It Works
Rootkits work by subverting the operating system itself — intercepting system calls, modifying kernel data structures, or hiding at a level below the OS entirely. There are several types based on where they operate:

- User-mode rootkit: runs in user space, hooks API calls to hide files, processes, and network connections from applications
- Kernel-mode rootkit: runs inside the OS kernel, most dangerous — can hide anything from the OS itself
- Bootkit: infects the Master Boot Record or bootloader, loads before the OS, invisible to everything running after
- Hypervisor rootkit: runs the compromised OS as a virtual machine underneath a malicious hypervisor

```bash
# example of what a user-mode rootkit does to hide a process
# normal ps output after rootkit is installed
ps aux | grep malware
# nothing shows up - rootkit intercepts the ps command output and removes its entries

# rootkit hides files the same way
ls /tmp/
# malicious files in /tmp are filtered out of the listing

# detection - check for discrepancies between tools
# if /proc shows a PID that ps doesn't, something is hiding it
ls /proc/ | grep -v "$(ps aux | awk '{print $2}')"
```

## Real-World Example
In 2005, Sony BMG shipped music CDs with a hidden rootkit that automatically installed on Windows machines when the CD was played. The rootkit hid any file or process with a name starting with `$sys$` from the OS — it was originally designed to prevent CD copying but created a massive security hole. Malware authors quickly released viruses that used the `$sys$` prefix to hide themselves completely. Sony had infected over 500,000 networks including military and government systems before the rootkit was discovered by security researcher Mark Russinovich using his own Sysinternals tools.

## Why It Matters
From an attacker's side, a rootkit turns temporary access into persistent invisible access. An attacker with a rootkit on a machine can maintain access for months or years, exfiltrate data continuously, and be extremely difficult to detect or remove. Nation-state threat actors commonly use kernel-level rootkits for long-term espionage.

From a defender's side, detecting rootkits is notoriously hard because you can't trust the OS they're running on — they control what the OS reports. Offline scanning (booting from a clean external drive) is more reliable than online scans. Secure Boot and UEFI firmware verification help prevent bootkits. Behavioral monitoring and integrity checking tools like Tripwire can catch anomalies before a rootkit fully establishes itself.

## Key Terms
- Rootkit: malware designed to maintain persistent privileged access while hiding its presence from the OS and security tools
- Kernel Mode: the highest privilege level in an OS where the core system code runs — kernel rootkits operate here
- Hooking: intercepting system calls or API functions to modify their behavior — how rootkits hide files and processes
- Bootkit: a rootkit that infects the bootloader and loads before the OS, making it invisible to OS-level detection
- Persistence: the ability of malware to survive reboots and maintain access over time

## One Tip / Tool

Tool: `chkrootkit` and `rkhunter` for Linux rootkit detection

```bash
# install and run chkrootkit
apt install chkrootkit
chkrootkit

# install and run rkhunter
apt install rkhunter
rkhunter --update
rkhunter --check
