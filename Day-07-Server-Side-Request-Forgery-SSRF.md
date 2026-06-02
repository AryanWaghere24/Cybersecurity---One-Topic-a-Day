# Day 07 - SSRF (Server-Side Request Forgery)

## What It Is
SSRF is a web attack where an attacker tricks a server into making HTTP requests to an unintended location — either internal network resources or external systems. Instead of the attacker's browser making the request directly, the vulnerable server makes it on their behalf. This lets attackers reach internal systems that are normally completely hidden from the outside world.
