# Day 06 - CSRF (Cross-Site Request Forgery)

## What It Is
CSRF is a web attack where an attacker tricks a logged-in user into unknowingly submitting a malicious request to a site they're already authenticated on. The site receives the request, sees a valid session, and executes it thinking the user intended it. The attacker doesn't need your password — they just hijack your existing trust with the site.
