# Day 46 - Search Engine Phishing (SEO Phishing)

## What It Is
SEO Phishing (Search Engine Phishing) is an attack where criminals create malicious websites optimized to rank high in search engine results for terms people commonly search — like "bank login", "PayPal sign in", or "Netflix account". When a victim searches for a legitimate service and clicks what appears to be the top result, they land on a convincing fake page designed to steal their credentials. Unlike most phishing attacks that come to the victim, SEO phishing waits for the victim to come to it — making it particularly insidious because the victim initiated the search themselves.

## How It Works
SEO phishing exploits user trust in search engine results — most people assume top results are legitimate, especially if they appear in paid ad spots or on the first page of organic results.

```
Two main delivery methods:

1. Malicious Paid Ads (most common currently)
Attackers purchase Google/Bing ads for high-value search terms
Ad appears above organic results with a URL that looks legitimate
Victim clicks the ad thinking it's the real site
Lands on a pixel-perfect clone of the real login page

Example:
Search: "chase bank login"
Ad result: "Chase Bank — Secure Login | chase-secure-login.com"
Real site: chase.com
The ad URL looks related but is a completely different domain

2. Organic SEO Manipulation
Creating content-rich fake pages that rank organically over time
Optimizing for long-tail keywords like "how to login to my wells fargo account"
Takes longer but costs nothing and is harder to take down quickly
Often uses compromised legitimate websites to host phishing content
```

Technical tactics attackers use:
```
- Typosquatting: registering domains with common misspellings
  (gooogle.com, paypa1.com, arnazon.com)
- Combosquatting: adding words to legitimate brand names
  (paypal-secure.com, apple-id-verify.com)
- Homograph attacks: using Unicode characters that look identical
  to ASCII (using Cyrillic 'а' instead of Latin 'a' in a domain)
- Ad cloaking: showing search engines a legitimate page during
  review but redirecting real visitors to the phishing page
```
## Real-World Example
In 2022 and 2023, security researchers documented widespread SEO phishing campaigns targeting cryptocurrency users. Fake pages for popular crypto wallets and exchanges appeared as sponsored ads in search results — sometimes above the legitimate site's own ads. Users searching to access their crypto accounts clicked these ads, entered their seed phrases or passwords on convincing clones, and lost their entire holdings. The FBI issued warnings specifically about this pattern after millions of dollars in cryptocurrency were stolen through search engine phishing campaigns targeting crypto platforms.
