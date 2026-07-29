# Day 58 - OSINT Techniques & Tools

## What It Is
OSINT (Open Source Intelligence) is the practice of collecting and analyzing publicly available information to gather intelligence about a target — a person, organization, domain, or infrastructure. "Open source" doesn't mean software — it means the information sources are openly accessible to anyone: search engines, social media, public records, DNS data, job postings, code repositories, and more. OSINT is used by both attackers (reconnaissance phase of the kill chain, day 22) and defenders (threat intelligence, finding exposed assets before attackers do). It requires no hacking, no illegal access — just knowing where to look and how to connect the dots.

## How It Works
OSINT follows a structured process — define what you're looking for, identify the right sources, collect systematically, and analyze to find actionable intelligence.

```
OSINT target categories and sources:

People / Individuals
- LinkedIn: job history, skills, connections, email patterns
- Twitter/X: opinions, location hints, associates, interests
- Facebook: personal details, family, location history
- Pipl, Spokeo: people search aggregators
- HaveIBeenPwned: check if email appeared in data breaches
- Reverse image search: find other accounts using same profile picture

Organizations
- Company website: employee names, email formats, technology stack
- LinkedIn company page: employee count, org structure, open roles
- Job postings: reveal internal technologies, security tools used
- SEC filings (public companies): financial data, acquisitions, subsidiaries
- Glassdoor reviews: internal culture, systems, processes
- Shodan: internet-facing infrastructure, open ports, banners

Domains & Infrastructure
- WHOIS: domain registration details, registrant info
- DNS records: subdomains, mail servers, IP ranges
- Certificate Transparency logs: all SSL certificates ever issued
- Shodan/Censys: open ports, running services, software versions
- BuiltWith/Wappalyzer: technology stack used by a website
- Wayback Machine: historical versions of websites

Code & Technical Intelligence
- GitHub: leaked credentials, internal tools, employee accounts
- Pastebin: data dumps, leaked credentials, internal data
- Google Dorks: advanced search operators to find exposed files
  site:company.com filetype:pdf "confidential"
  site:company.com inurl:admin
  "company.com" "password" filetype:txt
```
