# Day 08 - Privilege Escalation

## What It Is
Privilege Escalation is the process of gaining higher level permissions than what was originally granted on a system. An attacker who gets initial access as a low privilege user will almost always attempt to escalate to root (Linux) or SYSTEM/Administrator (Windows). It's not a single exploit - it's a category of techniques used after initial access to gain full control of a machine.

## How It Works
There are two types:

- Vertical Privilege Escalation: moving from a low privilege user to a higher one (regular user → root)
- Horizontal Privilege Escalation: accessing another user's resources at the same privilege level (user A accessing user B's files)

Common techniques for vertical escalation on Linux:

```bash
# 1. SUID binaries - files that run as root regardless of who executes them
find / -perm -u=s -type f 2>/dev/null

# 2. Sudo misconfigurations - check what you can run as root
sudo -l

# 3. Cron jobs running as root with writable scripts
cat /etc/crontab

# 4. Writable /etc/passwd - can add a new root user
ls -la /etc/passwd

# 5. Kernel exploits - outdated kernels with known CVEs
uname -a
```
