# Day 20 - RATs (Remote Access Trojans)

## What It Is
A Remote Access Trojan (RAT) is a type of malware that gives an attacker full remote control over a victim's machine through a hidden backdoor. Unlike a reverse shell (day 09) which is a basic command line connection, a RAT is a fully featured persistent implant — it survives reboots, hides itself, and provides capabilities like file management, keylogging, webcam access, screen capture, and more. The "Trojan" part means it disguises itself as legitimate software to trick the victim into running it.

## How It Works
A RAT has two components — the server (runs on the victim) and the client (runs on the attacker). The victim installs the server unknowingly, usually through a malicious email attachment, fake software download, or bundled with a cracked application. Once running it connects back to the attacker's client just like a reverse shell, but with a full GUI control panel.
