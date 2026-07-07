# Day 41 - Smishing

## What It Is
Smishing (SMS Phishing) is a phishing attack delivered through text messages instead of email. Attackers send fraudulent SMS messages impersonating banks, delivery companies, government agencies, or popular services to trick victims into clicking malicious links or calling fake numbers. The name combines "SMS" and "phishing." Smishing has grown significantly as smartphone usage increased — people tend to trust text messages more than emails and are less likely to scrutinize them carefully, making smishing increasingly effective compared to email phishing.

## How It Works
Smishing exploits the inherent trust people place in SMS messages and the limited context available on a mobile screen — you often can't hover over links to preview URLs, and sender information is easier to spoof or mask.

```
Common smishing pretexts:
- Package delivery: "Your USPS package could not be delivered.
  Track here: usps-delivery-update.com/track"

- Bank alerts: "ALERT: Unusual activity detected on your account.
  Verify immediately: secure-bankname-alert.com"

- Government notices: "IRS: You have a pending tax refund of $847.
  Claim before expiry: irs-refund-claim.net"

- Prize notifications: "You've won a $500 gift card!
  Claim in 24hrs: reward-claim-now.com"

- Two-factor bypass: "Your verification code is 847291.
  If you didn't request this reply STOP"
  (social engineering to get the victim to reveal their 2FA code)
```
Technical delivery methods:
```
SMS Spoofing    - sending SMS from a fake sender ID showing a bank name
                  or short code instead of a real phone number
SIM Swapping    - more advanced, convincing carrier to transfer victim's
                  number to attacker's SIM, intercepting all their SMS
Smishing Kits   - pre-built tools that automate sending bulk smishing
                  campaigns with tracking links
```
