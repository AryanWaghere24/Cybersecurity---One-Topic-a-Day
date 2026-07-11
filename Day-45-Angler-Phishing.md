# Day 45 - Angler Phishing

## What It Is
Angler Phishing is a social media based phishing attack where attackers create fake customer service accounts impersonating real brands and intercept complaints or queries posted publicly by frustrated customers. When someone tweets at their bank, posts a complaint about a delivery service, or asks a tech company for help on social media, attackers posing as that brand's support team respond with fake help — directing the victim to a phishing page or requesting sensitive account information. The name comes from the anglerfish, which dangles a lure to attract prey.

## How It Works
Angler phishing exploits the modern customer service expectation that brands respond to complaints on social media. Victims who post publicly are already frustrated, already expecting a response, and already primed to share account details to get their problem resolved.

![](assets/Angler-Phishing.md)

```
Attack flow:

Step 1 — Monitor social media for complaints
Attacker sets up alerts or bots monitoring mentions of target brands
Searches for: "@BankName I can't log in", "@Airline my booking is wrong"
Victims are already frustrated and expecting help

Step 2 — Create a convincing fake support account
Username: @BankName_Support_ or @BankNameHelp (extra underscore/word)
Profile picture: stolen from the real brand's official account
Bio: "Official customer support for @BankName — DM us for help"
Pinned posts: fake positive customer interactions

Step 3 — Intercept and respond faster than the real support team
Reply to the victim's complaint within minutes
"We're sorry to hear this! Please DM us your account details
so we can look into this right away."

Step 4 — Extract information in DMs
Once in private messages, request:
- Account number or username
- Password or security questions
- One-time verification codes (2FA bypass)
- Link to a fake "account verification" portal

Example fake vs real account:
Real:  @ChaseSupport (verified blue checkmark)
Fake:  @ChaseSupport_ (no checkmark, created last week, 12 followers)
```

## Real-World Example
Angler phishing became widely documented around 2015-2017 when researchers noticed fake airline and bank support accounts proliferating on Twitter. Passengers who tweeted complaints about cancelled flights were intercepted by fake airline support accounts that asked them to DM their booking reference, surname, and email — enough information to access and modify their booking or use in further targeted attacks. Some fake accounts were so convincing they accumulated thousands of followers before being reported and taken down, intercepting dozens of genuine customer complaints in the process.

## Why It Matters
From an attacker's side, angler phishing targets people at their most vulnerable — already frustrated, already expecting contact, and already in a mindset of sharing information to get their problem resolved. The public nature of social media complaints makes victims easy to identify and approach at exactly the right moment.

From a defender's side (organizations), registering and actively managing official support handles on all major platforms is critical — if you don't own @YourBrand_Support, an attacker will. Verifying your accounts where possible and clearly communicating your official support channels in your bio and pinned posts helps customers identify the real account. For individuals, always verify a support account's follower count, creation date, verification status, and whether it's linked from the brand's official website before sharing any account information.

## Key Terms
- Angler Phishing: intercepting public social media complaints to impersonate brand support and steal credentials
- Account Impersonation: creating a fake social media profile designed to be mistaken for a legitimate person or organization
- Social Media Monitoring: tracking brand mentions and keywords across platforms — used legitimately by brands, abused by attackers for angler phishing
- Verified Badge: a platform-granted indicator (checkmark) confirming an account's authenticity — absence is a red flag for support accounts
- DM Phishing: moving a conversation to direct messages where the attack is less visible to the public and other users

## One Tip / Tool

Tool: No specific attack tool — angler phishing is manual. For defense, `Google Alerts` and `Mention.com` help brands monitor for impersonation attempts

```
How to spot a fake support account:
1. Check account creation date — real support accounts are old
2. Check follower count — legitimate brand support has thousands
3. Look for verification badge — major brands are usually verified
4. Check if the account is linked from the brand's official website
5. Look at their tweet history — fake accounts have little history
6. The real support handle is usually in the brand's official bio

If you're posting a complaint publicly:
- Navigate directly to the brand's official website to find support
- Check the brand's official account bio for their support handle
- Be suspicious of any account that replies to your complaint
  asking you to DM account details within minutes of your post
```

Angler phishing is a reminder that the attack surface has expanded far beyond email — anywhere people interact with brands publicly online is a potential vector for social engineering. The attacker's advantage is speed and the victim's existing emotional state. Taking a moment to verify before sharing anything in a DM removes that advantage entirely.
