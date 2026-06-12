# Day 17 - Pass the Hash

## What It Is
Pass the Hash (PtH) is an attack where an attacker uses a stolen NTLM password hash to authenticate to a system without knowing or cracking the actual plaintext password. Windows authentication protocols accept the hash directly as proof of identity — so if you have the hash, you have access. It turns hash dumping from a stepping stone into a final destination.

## How It Works
Windows uses NTLM hashes for authentication in many scenarios — local logins, network shares, remote desktop, and more. When you log in, Windows doesn't send your plaintext password — it sends the NTLM hash as the credential. An attacker who steals that hash can replay it to authenticate as that user anywhere the hash is accepted.
