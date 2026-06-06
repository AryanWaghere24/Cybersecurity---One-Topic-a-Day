# Day 11 - WPA2 Cracking

## What It Is
WPA2 (Wi-Fi Protected Access 2) is the security protocol used to protect most modern Wi-Fi networks. WPA2 cracking is the process of capturing the authentication handshake between a device and a router, then using offline brute force or dictionary attacks to recover the original password from it. The attacker never needs to interact with the router again after capturing the handshake — all the cracking happens locally.

## How It Works
When a device connects to a WPA2 network, a 4-way handshake happens between the device and the router. This handshake doesn't transmit the actual password but contains enough cryptographic material that if you capture it, you can test password guesses against it offline.

Attack flow:
1. Put the wireless adapter into monitor mode to capture raw wireless traffic
2. Identify the target network and its channel
3. Capture the 4-way handshake — either by waiting for a device to connect or by sending a deauth packet to force a reconnection
4. Take the captured handshake offline and run a dictionary or brute force attack against it
5. If the password is in your wordlist, it gets cracked

```bash
# Step 1 - enable monitor mode
airmon-ng start wlan0

# Step 2 - scan for networks
airodump-ng wlan0mon

# Step 3 - capture handshake on target network
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# Step 4 - force a deauth to speed up handshake capture
aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon

# Step 5 - crack the handshake with a wordlist
aircrack-ng capture.cap -w /usr/share/wordlists/rockyou.txt
```

## Real-World Example
WPA2 cracking is one of the first things covered in any wireless pentesting engagement. A pentester on a red team assessment parks outside a target office, puts their wireless adapter in monitor mode, captures the handshake when an employee's laptop reconnects after a deauth, and takes it back to crack offline using rockyou.txt or a custom wordlist. Weak passwords like `company2024` or `Welcome123` get cracked in seconds. Strong random passwords can take years or never get cracked at all — which is exactly why password strength matters so much for Wi-Fi.
