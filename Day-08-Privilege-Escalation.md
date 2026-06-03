# Day 08 - Privilege Escalation

## What It Is
Privilege Escalation is the process of gaining higher level permissions than what was originally granted on a system. An attacker who gets initial access as a low privilege user will almost always attempt to escalate to root (Linux) or SYSTEM/Administrator (Windows). It's not a single exploit - it's a category of techniques used after initial access to gain full control of a machine.

## How It Works
There are two types:

- Vertical Privilege Escalation: moving from a low privilege user to a higher one (regular user → root)
- Horizontal Privilege Escalation: accessing another user's resources at the same privilege level (user A accessing user B's files)

Common techniques for vertical escalation on Linux:
