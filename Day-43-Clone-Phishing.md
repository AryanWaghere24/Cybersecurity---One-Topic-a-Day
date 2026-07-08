# Day 43 - Clone Phishing

## What It Is
Clone Phishing is a type of phishing attack where the attacker takes a legitimate email that the victim has previously received — from a bank, a service provider, or a colleague — and creates an almost identical copy of it, replacing the real links or attachments with malicious ones. The cloned email is then sent to the victim appearing to come from the original sender. Because the email looks exactly like something the victim has already seen and trusted before, it's significantly more convincing than a generic phishing attempt.

## How It Works
Clone phishing exploits familiarity — victims recognize the email format, the sender name, and the content because they've seen the real version before. The attacker intercepts or obtains a copy of a legitimate email, makes minimal changes, and resends it.

```
Clone phishing attack flow:

Step 1 — Obtain a legitimate email
Attacker gets a real email the victim received previously
Sources: compromised email accounts, data breaches, 
         publicly visible email threads, or guessing common 
         transactional emails (order confirmations, password resets)

Step 2 — Clone it
Copy the exact layout, branding, subject line, and content
Replace only the links or attachments with malicious versions
Keep everything else identical — same logo, same footer, same tone

Step 3 — Craft a convincing resend pretext
"Resending this as the previous link expired"
"Updated attachment — please use this version instead"
"We noticed you didn't open our previous email, here it is again"

Step 4 — Spoof the sender
Send from a lookalike domain or compromised account
Victim sees familiar content from a familiar-looking sender

Real vs cloned email comparison:
Original: "Your Adobe sign document is ready — Sign here [legitimate link]"
Cloned:   "Your Adobe sign document is ready — Sign here [malicious link]"
Everything looks identical — only the destination URL differs
```
