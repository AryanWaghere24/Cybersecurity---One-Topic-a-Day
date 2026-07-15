# Day 48 - Pharming

## What It Is
Pharming is an attack that redirects users to a fake malicious website without them clicking any suspicious link — even when they type the correct URL directly into their browser. Unlike phishing which requires the victim to click something, pharming corrupts the DNS resolution process itself, so typing "paypal.com" correctly takes you to an attacker-controlled fake page instead of the real one. It's considered more dangerous than regular phishing because the victim does everything right — they type the correct address — and still end up on a malicious site.

## How It Works
Pharming exploits the DNS (Domain Name System) infrastructure that translates domain names into IP addresses. There are two main attack methods:

```
Method 1 — Local Hosts File Poisoning
Every computer has a local hosts file that maps domain names to IPs
If an attacker can modify this file (via malware), they can redirect
any domain to their own server directly on the victim's machine

Location of hosts file:
Windows: C:\Windows\System32\drivers\etc\hosts
Linux/Mac: /etc/hosts

Poisoned hosts file example:
192.168.1.100   paypal.com      ← attacker's IP instead of PayPal's real IP
192.168.1.100   bankofamerica.com
192.168.1.100   gmail.com
