# Day 26 - Burp Suite Deep Dive

## What It Is
Burp Suite is the industry standard intercepting proxy and web application security testing platform, built by PortSwigger. It sits between your browser and the target web application, letting you intercept, inspect, and modify every HTTP request and response in real time. While we've referenced Burp Suite earlier in this repo (CSRF PoC generation on day 06), today covers the full toolset that makes it the primary tool for almost every web app pentest in the industry.

## How It Works
Burp Suite is made up of several integrated tools that work together around a core proxy:

```
Proxy        - intercepts and modifies traffic between browser and target
Repeater     - resend and manually modify individual requests repeatedly
Intruder     - automate sending many requests with varying payloads (fuzzing, brute force)
Decoder      - encode/decode data (Base64, URL encoding, hex) instantly
Comparer     - diff two requests or responses to spot subtle differences
Sequencer    - analyze randomness in session tokens for predictability
Extender     - install community plugins (BApps) to extend functionality
```
Basic workflow for testing a login form:
```
1. Configure browser to proxy through Burp (default 127.0.0.1:8080)
2. Submit a login request through the browser
3. Burp's Proxy tab intercepts the raw HTTP request before it's sent
4. Right click → "Send to Repeater" to manually test variations
5. In Repeater, modify parameters and resend instantly to observe responses
6. If testing for brute force, send the request to Intruder instead
7. In Intruder, mark the password field as a payload position
8. Load a wordlist and start the attack — Burp sends hundreds of requests automatically
9. Sort results by response length or status code to spot the successful login
```

This single workflow alone can test for SQL Injection (day 04), broken authentication (day 06 CSRF related), and brute force vulnerabilities all from the same captured request.

## Real-World Example
In professional web app pentesting, almost every finding starts in Burp's Proxy history. A pentester testing an e-commerce site notices a request containing `price=49.99` when adding an item to cart. They send it to Repeater, change the value to `price=0.01`, resend it, and the server accepts it without validation — a critical business logic flaw allowing anyone to set their own prices. This exact kind of manual testing, impossible to fully automate, is why Burp Suite remains essential even with modern automated scanners.
