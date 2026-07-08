# Day 42 - Vishing

## What It Is
Vishing (Voice Phishing) is a phishing attack conducted over phone calls where attackers impersonate trusted entities — banks, government agencies, tech support, or internal IT departments — to manipulate victims into revealing sensitive information or taking harmful actions. The name combines "voice" and "phishing." Vishing is particularly effective because a real human voice creates a stronger sense of urgency and authority than a text or email, making it harder for victims to pause and think critically before complying.

## How It Works
Vishing attacks rely heavily on social engineering principles — authority, urgency, and fear — amplified by the real-time pressure of a live phone conversation. Attackers use caller ID spoofing to make the call appear to come from a legitimate number.

```
Common vishing pretexts:

Bank Fraud Department:
"This is Visa security calling. We've detected a $2,400 charge 
from Amazon on your card. To prevent further fraud we need to 
verify your identity. Can you confirm your full card number?"

Tech Support Scam:
"This is Microsoft technical support. We've detected a virus 
on your computer sending data to hackers. I need remote access 
to fix this immediately before your data is stolen."

Government/IRS Scam:
"This is the IRS. You have unpaid taxes of $3,200. 
A warrant has been issued for your arrest. 
Call this number immediately to resolve before officers arrive."

Internal IT:
"Hi, this is the helpdesk. We're doing a security audit and 
need to verify your credentials to complete the system update."

Techniques used during the call:
- Caller ID spoofing to show a legitimate bank/government number
- Background noise of fake call centers to seem authentic
- Urgency and fear to prevent the victim from hanging up and verifying
- Keeping the victim on the line while a second attacker attempts account access
```
## Real-World Example
The 2020 Twitter hack (also referenced in day 36) involved vishing as its primary attack vector. Attackers called Twitter employees posing as internal IT support, using information gathered from LinkedIn to make the calls convincing — addressing employees by name, referencing real internal systems, and creating urgency about a "VPN issue." Employees were directed to a fake internal Twitter VPN portal where they entered their credentials. Those credentials were then used to access Twitter's admin tools, leading to the takeover of high-profile verified accounts. The entire breach of one of the world's most visited platforms started with phone calls.

## Why It Matters
From an attacker's side, vishing is highly effective because real-time conversation creates immediate psychological pressure. Victims can't take time to verify, can't forward the call to a security team, and the human voice triggers instinctive trust responses that text-based attacks don't. Modern AI voice cloning technology is making vishing even more dangerous — attackers can now clone an executive's voice from publicly available audio and call employees impersonating them.

From a defender's side, the core defense is the same as all social engineering — verify through a separate channel. Hang up and call the organization back on their official published number. No legitimate bank, government agency, or IT department will pressure you to stay on the line and prevent you from verifying their identity. Security awareness training that specifically includes vishing scenarios is essential since most training focuses on email phishing.

## Key Terms
- Vishing (Voice Phishing): phishing attacks conducted over phone calls using social engineering to extract information
- Caller ID Spoofing: making a phone call appear to come from a different number than the actual origin
- Voice Cloning: using AI to generate a synthetic replica of a real person's voice from audio samples
- Tech Support Scam: a specific vishing pretext where attackers impersonate technical support to gain remote access or extract payment
- Pretexting: creating a fabricated believable scenario before making the vishing call

## One Tip / Tool

Tool: `SpoofCard` and similar services are what attackers abuse for caller ID spoofing — for defenders, **call verification procedures** are the primary defense

```
Vishing defense checklist:
1. Never provide sensitive information to inbound callers
   regardless of what number appears on caller ID
2. If a caller claims to be from your bank — hang up,
   call the number on the back of your card directly
3. No legitimate organization will threaten immediate arrest
   or account closure if you don't comply instantly
4. If an "IT employee" calls asking for credentials — verify
   by calling your IT helpdesk on their known internal number
5. Report vishing attempts to the FTC at reportfraud.ftc.gov

Red flags during a call:
- Urgency and pressure to act immediately
- Threats of arrest, account closure, or legal action
- Requests for gift card payments (common in scams)
- Asking you to stay on the line and not call anyone else
- Requesting remote access to your computer
```

The rise of AI voice cloning means that even hearing a familiar voice on a phone call is no longer sufficient verification. Organizations should establish safe word verification systems for sensitive requests made over phone — a pre-agreed code word that proves the caller is genuinely who they claim to be, not an AI clone of their voice.
