# Day 36 - Social Engineering

## What It Is
Social Engineering is the practice of manipulating people into revealing confidential information or performing actions that compromise security — without ever touching a single line of code. Instead of exploiting software vulnerabilities, social engineers exploit human psychology: trust, authority, urgency, fear, and helpfulness. It's consistently responsible for the majority of successful cyberattacks because no matter how strong your technical defenses are, humans remain the most exploitable attack surface.

## How It Works
Social engineering attacks follow a predictable psychological framework — establish trust, create a pretext, exploit a human bias, and extract what you need. The attacker researches the target first (OSINT, LinkedIn, company website) to make the attack believable.

Core psychological principles exploited:

```
Authority     - people comply with those who appear to be in positions of power
               "This is the IT department, we need your credentials to fix your account"

Urgency       - time pressure bypasses rational thinking
               "Your account will be suspended in 30 minutes unless you verify now"

Social Proof  - people follow what others around them do
               "Everyone else on your team has already completed this verification"

Reciprocity   - people feel obligated to return favors
               Attacker provides something helpful first, then makes a request

Liking        - people comply more with those they like or relate to
               Building rapport before making the actual malicious request

Fear          - threat of negative consequences drives hasty action
               "Your system is infected, click here immediately to fix it"
```

## Real-World Example
The 2020 Twitter hack is one of the most famous social engineering attacks in recent history. Attackers called Twitter employees posing as the internal IT department, convincing them to provide credentials to an internal admin tool. Once inside, they took over verified accounts including Barack Obama, Elon Musk, and Apple to run a Bitcoin scam. The entire attack bypassed all of Twitter's technical security infrastructure — no vulnerability was exploited, no code was written. A phone call and a convincing pretext was all it took to compromise one of the world's most high profile platforms.

## Why It Matters
From an attacker's side, social engineering is the most cost-effective attack vector — it requires no technical knowledge, no expensive tools, and bypasses even the most sophisticated technical defenses. A single successful phishing email or phone call can hand over credentials that would take weeks to crack technically.
