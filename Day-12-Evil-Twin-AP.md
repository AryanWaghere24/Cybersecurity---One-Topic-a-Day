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
