# Day 19 - Keyloggers

## What It Is
A Keylogger is a type of malware that records every keystroke made on a device and sends the captured data to the attacker. Every password you type, every message you send, every search you make — all of it gets silently logged. It's one of the oldest and most effective forms of credential theft because it captures passwords at the source, before any encryption kicks in.

## How It Works
Keyloggers operate at different levels depending on their type:

- Software keyloggers: run as a background process, hook into the OS keyboard input APIs to intercept keystrokes before they reach the application
- Kernel keyloggers: operate at kernel level, harder to detect, intercept keystrokes at the driver level
- Hardware keyloggers: physical devices plugged between the keyboard and the computer, completely invisible to the OS and any software
- Browser keyloggers: malicious browser extensions that capture input only inside the browser
