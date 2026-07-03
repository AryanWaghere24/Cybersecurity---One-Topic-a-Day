# Day 38 - Email Phishing

## What It Is
Email Phishing is the most common form of phishing where attackers send fraudulent emails impersonating legitimate organizations — banks, tech companies, government agencies, or internal IT departments — to trick recipients into clicking malicious links, downloading malware, or providing sensitive information. It's the oldest and most widely used cyberattack delivery method, accounting for the majority of all phishing attacks globally. Despite being well known, it remains devastatingly effective because attackers continuously refine their techniques to bypass both technical filters and human suspicion.

## How It Works
A phishing email is engineered to look as legitimate as possible while hiding its malicious intent. Attackers abuse several techniques to make emails convincing:

```
Email Spoofing Techniques:
- Display name spoofing: "PayPal Security" <attacker@gmail.com>
  The name looks legitimate but the actual address reveals the fraud

- Lookalike domains: support@paypa1.com, security@arnazon.com
  Characters replaced with visually similar ones (1 instead of l, rn instead of m)

- Subdomain abuse: paypal.com.attacker-site.com
  Real brand name appears in the URL but the actual domain is attacker-site.com

- Legitimate service abuse: sending phishing content through 
  Google Docs, OneDrive, or Dropbox links that pass email filters
  since the sending domain is genuinely legitimate
