# Day 12 - Evil Twin AP

## What It Is
An Evil Twin AP (Access Point) is a rogue wireless access point that impersonates a legitimate Wi-Fi network by broadcasting the same SSID (network name). Victims connect to it thinking it's the real network — their coffee shop Wi-Fi, office network, or home router. Once connected, all their traffic flows through the attacker's machine, enabling full MITM attack, credential theft, and traffic manipulation.

## How It Works
Every Wi-Fi network is identified by its SSID. Devices that have connected before will automatically reconnect when they see the same SSID. Evil Twin exploits this auto-connect behavior.

Attack flow:
1. Attacker scans for nearby networks and picks a target SSID
2. Attacker sets up a fake AP broadcasting the same SSID on a stronger signal
3. Optionally sends deauth packets to kick devices off the real AP (see day 13)
4. Victim's device auto-connects to the stronger fake AP
5. Attacker serves a captive portal (fake login page) asking for Wi-Fi password
6. Victim enters the password — attacker captures it in plaintext
7. All traffic now flows through the attacker — full MITM position

```bash
# using hostapd-wpe to set up a rogue AP
# first create hostapd config
cat > evil_twin.conf << EOF
interface=wlan0
driver=nl80211
ssid=TargetNetwork
channel=6
EOF

# start the fake AP
hostapd evil_twin.conf

# use dnsmasq to handle DHCP so victims get an IP
dnsmasq --interface=wlan0 --dhcp-range=192.168.1.2,192.168.1.30
```

## Real-World Example
At DEF CON, the world's largest hacking conference, Evil Twin attacks are so common that experienced attendees avoid connecting to any Wi-Fi at all. Attackers set up fake APs mimicking the conference Wi-Fi, hotel Wi-Fi, and nearby coffee shops. Unsuspecting attendees connect, get served a captive portal, and hand over credentials without realizing. It's become such a known risk that DEF CON itself warns attendees to treat all wireless networks as hostile.

On real engagements, a pentester will set up an Evil Twin outside a target building mimicking the corporate SSID. Employees stepping outside or in parking lots whose laptops auto-connect give the attacker a direct MITM position into corporate traffic.

## Why It Matters
From an attacker's side, Evil Twin requires no password cracking and no prior knowledge of the network key. A stronger signal always wins — devices connect to the AP with the best signal regardless of which one is legitimate. Combined with a deauth attack it becomes nearly impossible for victims to stay on the real network.

From a defender's side, using a VPN on all networks is the strongest personal defense — even if you connect to an Evil Twin, your traffic is encrypted end to end. Enterprise networks use 802.1X authentication (WPA2-Enterprise) which requires certificate-based authentication, making Evil Twin much harder to pull off. Users should also disable auto-connect for public Wi-Fi networks.

## Key Terms
- Evil Twin AP: a rogue access point that clones a legitimate network's SSID to trick devices into connecting
- SSID (Service Set Identifier): the name of a Wi-Fi network that devices use to identify and connect to it
- Captive Portal: a web page shown to newly connected users, often used legitimately by hotels and cafes, abused by attackers to steal credentials
- 802.1X: enterprise Wi-Fi authentication standard that uses certificates instead of passwords, resistant to Evil Twin
- Rogue AP: any unauthorized access point on a network, Evil Twin is a specific type of rogue AP

## One Tip / Tool

Tool: `airbase-ng` (part of aircrack-ng suite) or `hostapd-wpe` for setting up rogue APs

```bash
# quick evil twin with airbase-ng
airmon-ng start wlan0
airbase-ng -e "TargetSSID" -c 6 wlan0mon

# the above creates a tap interface at0
# bring it up and assign IP
ifconfig at0 up 192.168.1.1 netmask 255.255.255.0

# run dnsmasq for DHCP
dnsmasq --interface=at0 --dhcp-range=192.168.1.2,192.168.1.100,12h
```

For a more complete automated Evil Twin attack with captive portal, **WiFi-Pumpkin3** is a dedicated framework that handles AP creation, DHCP, DNS spoofing, and credential harvesting all in one tool. Only use on networks you own or have explicit permission to test on.
