# Day 09 - Reverse Shell

## What It Is
A Reverse Shell is a technique where the target machine initiates a connection back to the attacker's machine, giving the attacker an interactive command line session on the victim. Unlike a regular shell where you connect to a server, here the server connects to you. It's called "reverse" because the connection direction is flipped — the victim reaches out, the attacker listens.

## How It Works
Firewalls typically block incoming connections to a machine but allow outgoing ones. A bind shell (where the attacker connects to the victim) would get blocked. A reverse shell bypasses this because the victim machine makes the outgoing connection itself — which firewalls usually allow.

Attack flow:
1. Attacker sets up a listener on their machine waiting for incoming connections
2. Attacker gets code execution on the victim — through a web shell, exploit, phishing, or any other vulnerability
3. Attacker runs a reverse shell payload on the victim machine
4. Victim machine connects back to the attacker's IP and port
5. Attacker gets an interactive terminal session on the victim
