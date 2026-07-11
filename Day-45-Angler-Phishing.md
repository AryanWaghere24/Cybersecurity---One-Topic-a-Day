# Day 45 - Angler Phishing

## What It Is
Angler Phishing is a social media based phishing attack where attackers create fake customer service accounts impersonating real brands and intercept complaints or queries posted publicly by frustrated customers. When someone tweets at their bank, posts a complaint about a delivery service, or asks a tech company for help on social media, attackers posing as that brand's support team respond with fake help — directing the victim to a phishing page or requesting sensitive account information. The name comes from the anglerfish, which dangles a lure to attract prey.

## How It Works
Angler phishing exploits the modern customer service expectation that brands respond to complaints on social media. Victims who post publicly are already frustrated, already expecting a response, and already primed to share account details to get their problem resolved.

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
