# Day 14 - PMKID Attack

## What It Is
The PMKID Attack is a modern WPA2 cracking technique discovered in 2018 by Jens Steube (the creator of hashcat). Unlike traditional WPA2 cracking which requires capturing a 4-way handshake by waiting for a client to connect, PMKID lets you attack the router directly with no clients needed. You just need one single frame from the router and you can crack the password offline. It made WPA2 cracking significantly faster and easier.

## How It Works
The PMKID is a value the router includes in the first frame of the EAPOL authentication process. It's calculated using:

```
PMKID = HMAC-SHA1-128(PMK, "PMK Name" + AP_MAC + Client_MAC)
```

The PMK (Pairwise Master Key) is derived directly from the Wi-Fi password. So if you can obtain the PMKID from the router and crack the PMK offline, you get the password.

Attack flow:
1. Attacker sends an EAPOL frame request to the router
2. Router responds with a single frame containing the PMKID
3. Attacker takes that PMKID value offline
4. Runs a dictionary or brute force attack to find the PMK that produces the same PMKID
5. Password recovered — no clients, no handshake waiting required
