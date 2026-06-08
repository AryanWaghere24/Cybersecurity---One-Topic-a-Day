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

```bash
# Step 1 - install hcxdumptool and hcxtools
apt install hcxdumptool hcxtools

# Step 2 - capture PMKID from router (no clients needed)
hcxdumptool -i wlan0mon -o capture.pcapng --enable_status=1

# Step 3 - convert to hashcat format
hcxpcapngtool -o hash.hc22000 capture.pcapng

# Step 4 - crack with hashcat
hashcat -m 22000 hash.hc22000 /usr/share/wordlists/rockyou.txt
```

## Real-World Example
Before PMKID, a pentester targeting a Wi-Fi network with no active clients had to wait — sometimes hours — for a device to connect naturally or rely on deauth attacks to force a reconnection. After Jens Steube published the PMKID technique in 2018, the game changed completely. Now a pentester can drive through a neighborhood, collect PMKIDs from every router they pass, and crack them all offline later with no interaction with any client device. The attack works against the majority of routers that support the RSN IE (Robust Security Network Information Element) in their beacon frames.
