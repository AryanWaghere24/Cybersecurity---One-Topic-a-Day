# Day 25 - Metasploit Framework

## What It Is
Metasploit is the most widely used open source exploitation framework in cybersecurity. It provides a massive library of exploits, payloads, and auxiliary modules that let security professionals find, exploit, and validate vulnerabilities in a structured way. Instead of writing exploit code from scratch every time, Metasploit gives you a ready-made framework where exploits, payloads, and post-exploitation tools all work together seamlessly.

## How It Works
Metasploit organizes everything into modules. The core workflow is search for a module, configure it, and run it.

```
Module Types:
- Exploits     - code that takes advantage of a specific vulnerability
- Payloads     - the code that runs after successful exploitation (e.g. meterpreter, day 20)
- Auxiliary    - scanning, fuzzing, and other supporting modules (not exploits themselves)
- Post         - post-exploitation modules (privilege escalation, day 08, credential dumping, day 17)
- Encoders     - obfuscate payloads to evade detection
