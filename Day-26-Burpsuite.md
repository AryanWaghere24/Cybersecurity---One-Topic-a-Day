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
