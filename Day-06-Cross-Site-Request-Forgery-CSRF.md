# Day 06 - CSRF (Cross-Site Request Forgery)

## What It Is
CSRF is a web attack where an attacker tricks a logged-in user into unknowingly submitting a malicious request to a site they're already authenticated on. The site receives the request, sees a valid session, and executes it thinking the user intended it. The attacker doesn't need your password — they just hijack your existing trust with the site.

## How It Works
When you log into a site, your browser stores a session cookie. Every request you make to that site automatically includes that cookie. CSRF exploits this — if the attacker can get your browser to send a request to that site, it will include your cookie automatically and the site won't know the difference.

Attack flow:
1. Victim logs into bank.com, session cookie is stored in browser
2. Without logging out, victim visits a malicious page or clicks an attacker's link
3. That page contains a hidden request targeting bank.com — like a fund transfer form
4. Victim's browser fires the request automatically, cookie gets attached
5. Bank.com sees a valid session and processes the transfer
6. Victim never knew it happened

A hidden form that auto-submits looks like this:
```html
<!-- Hidden on attacker's page, fires automatically on load -->
<form action="https://bank.com/transfer" method="POST">
  <input type="hidden" name="amount" value="10000"/>
  <input type="hidden" name="to" value="attacker_account"/>
</form>
<script>document.forms[0].submit()</script>
```
## Real-World Example
In 2008, a CSRF vulnerability was found in ING Direct, an online banking site. An attacker could craft a malicious page that when visited by a logged-in ING customer, would silently initiate a fund transfer to the attacker's account. The bank's server saw a valid session cookie and processed it as a legitimate request. The customer would have no idea until they checked their balance.

## Why It Matters
From an attacker's side, CSRF requires almost no technical skill to exploit once a vulnerable endpoint is found. A simple HTML page with a hidden form is enough. It can be used for fund transfers, email/password changes, admin actions — anything the logged-in user can do, the attacker can do through them.

From a defender's side, the standard fix is CSRF tokens — a unique random value tied to the user's session that must be included in every state-changing request. Since the attacker's page can't read this token (due to same-origin policy), the forged request gets rejected. The `SameSite` cookie attribute is another modern defense that prevents cookies from being sent on cross-site requests.

## Key Terms
- CSRF (Cross-Site Request Forgery): tricking a logged-in user's browser into sending an unintended request to a trusted site
- Session Cookie: a token stored in the browser that keeps you logged in between requests
- CSRF Token: a secret random value embedded in forms that servers verify to confirm the request is legitimate
- Same-Origin Policy: browser security rule that prevents one site from reading data from another site
- SameSite Cookie: cookie attribute that controls whether cookies are sent with cross-site requests

## One Tip / Tool

Tool: Burp Suite (the go-to tool for web app pentesting)

```
1. Intercept a legitimate POST request in Burp Suite
2. Right click the request
3. Select "Engagement tools" → "Generate CSRF PoC"
4. Burp auto-generates the malicious HTML form for you
5. Open it in a browser while logged into the target site to test
```

Quick manual test - check if any state-changing request (transfer, password change, delete) is missing a CSRF token in the POST body or headers. If there's no token, the endpoint is likely vulnerable.
