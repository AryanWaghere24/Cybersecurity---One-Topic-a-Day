# Day 19 - Keyloggers

## What It Is
A Keylogger is a type of malware that records every keystroke made on a device and sends the captured data to the attacker. Every password you type, every message you send, every search you make — all of it gets silently logged. It's one of the oldest and most effective forms of credential theft because it captures passwords at the source, before any encryption kicks in.

## How It Works
Keyloggers operate at different levels depending on their type:

- Software keyloggers: run as a background process, hook into the OS keyboard input APIs to intercept keystrokes before they reach the application
- Kernel keyloggers: operate at kernel level, harder to detect, intercept keystrokes at the driver level
- Hardware keyloggers: physical devices plugged between the keyboard and the computer, completely invisible to the OS and any software
- Browser keyloggers: malicious browser extensions that capture input only inside the browser

```python
# simple software keylogger in Python using pynput
from pynput.keyboard import Key, Listener
import logging

logging.basicConfig(filename='keylog.txt', level=logging.DEBUG, format='%(asctime)s: %(message)s')

def on_press(key):
    try:
        logging.info(str(key.char))
    except AttributeError:
        logging.info(str(key))

with Listener(on_press=on_press) as listener:
    listener.join()
```

This runs silently in the background and logs every keystroke with a timestamp to a file. A real keylogger would also exfiltrate the log file periodically to the attacker's server.

## Real-World Example
In 2015, a keylogger was found inside point-of-sale systems at Trump Hotels. Attackers had installed keylogging malware on the hotel's payment systems that captured credit card details as staff typed them in. The breach affected properties across multiple cities and exposed customer payment data over several months before being discovered.

Hardware keyloggers are also common in physical pentests — a red teamer can plug a tiny hardware keylogger into the back of a desktop in a few seconds while pretending to plug in a USB drive, and come back later to retrieve it with weeks of captured credentials.

## Why It Matters
From an attacker's side, keyloggers bypass all encryption because they capture input before it's encrypted. It doesn't matter if a site uses HTTPS — the password is captured as you type it, before it ever gets sent. They're also effective against 2FA if the attacker logs in fast enough after capturing the credentials.

From a defender's side, endpoint detection and response (EDR) tools monitor for suspicious keyboard hooking behavior. Virtual keyboards (on-screen keyboards) can bypass software keyloggers since no physical keystroke is made. Password managers that autofill credentials also help since the password is never actually typed. Regular security audits for physical access points are important to catch hardware keyloggers.

## Key Terms
- Keylogger: malware that records and exfiltrates every keystroke made on a device.
- Keystroke Logging: the act of capturing keyboard input silently in the background.
- API Hooking: intercepting calls to OS functions — how software keyloggers intercept keyboard input.
- Hardware Keylogger: a physical device that sits between keyboard and computer, invisible to any software.
- EDR (Endpoint Detection and Response): security software that monitors endpoints for suspicious behavior including keyboard hooking.
