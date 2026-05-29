# Day 03 - SSL Stripping

## What It Is
SSL Stripping is an attack that downgrades a secure HTTPS connection to plain HTTP without the victim realizing it. The attacker sits between the victim and the server, talking HTTPS with the server but serving plain HTTP to the victim. Everything the victim sends - passwords, session tokens, personal data - goes out unencrypted.

## How It Works
When you visit a site, your browser often starts with HTTP first and then gets redirected to HTTPS. SSL Stripping hijacks that exact moment before the secure connection is established.

The attack flow:
1. Attacker is already in the middle (via ARP Spoofing for example)
2. Victim's browser sends an HTTP request to bank.com
3. Attacker intercepts it and makes the HTTPS request to bank.com on the victim's behalf
4. Attacker receives the encrypted response from the server
5. Attacker strips the HTTPS and forwards plain HTTP back to the victim
6. Victim's browser shows bank.com over HTTP, victim never sees the padlock
7. Attacker can now read everything in plaintext

The server thinks it's talking securely to the user. The user thinks they're on the real site. Only the attacker sees both sides in plaintext.

## Real-World Example
You're on hotel Wi-Fi and an attacker is already running ARP Spoofing on the network. You open your browser and type facebook.com - your browser first hits HTTP, the attacker intercepts, strips SSL, and serves you the HTTP version. You log in, your credentials go out in plaintext, attacker captures them. The URL bar might just show http://facebook.com and if you're not paying attention you'd never notice.

This is exactly why the three attacks chain together - ARP Spoofing (day 01) gets the attacker in the middle, DNS Spoofing (day 02) can redirect you to a fake site, and SSL Stripping (day 03) removes your encryption layer.

## Why It Matters
From an attacker's side, SSL Stripping is powerful because most users don't actively check for the padlock or HTTPS in the URL bar. Combined with a MITM position it can silently capture credentials from dozens of users on a shared network.

From a defender's side, HSTS (HTTP Strict Transport Security) was specifically built to counter this. Sites that implement HSTS tell browsers to never connect over HTTP, ever. Browsers that have visited the site before will refuse a plain HTTP connection outright, breaking the attack. HSTS Preloading takes it further by hardcoding sites into the browser itself.

## Key Terms
- SSL/TLS: protocols that encrypt communication between browser and server (HTTPS uses TLS)
- SSL Stripping: downgrading a connection from HTTPS to HTTP to expose plaintext traffic
- MITM (Man-in-the-Middle): attacker secretly sits between two communicating parties
- HSTS (HTTP Strict Transport Security): a header that forces browsers to always use HTTPS for a domain
- HSTS Preload: a list built into browsers of sites that must always use HTTPS, even on first visit

## One Tip / Tool

Tool: `sslstrip` by Moxie Marlinspike (the researcher who originally demonstrated this attack)

```bash
# first get in the middle with ARP spoofing (see day 01)
# redirect HTTP traffic to sslstrip
iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080

# run sslstrip on port 8080
sslstrip -l 8080
```

Detection tip: always check for HTTPS and the padlock before entering credentials. If a site you know uses HTTPS is loading over HTTP, something is wrong. You can also check if a site has HSTS enabled by looking at its response headers - `Strict-Transport-Security` should be present.
