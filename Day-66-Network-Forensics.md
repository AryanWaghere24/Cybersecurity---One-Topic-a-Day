# Day 66 - Network Forensics

## What It Is
Network Forensics is the capture, recording, and analysis of network traffic to investigate security incidents, detect intrusions, and reconstruct attacker communications. While disk forensics (day 63) examines what happened on a system and memory forensics (day 62) captures what was running, network forensics answers different questions — what data left the network, what systems did the attacker communicate with, how did the malware spread laterally, and what commands were sent to compromised systems. Network traffic is the most complete record of attacker activity that crosses network boundaries, making it invaluable for investigating breaches involving data exfiltration, C2 communications, and lateral movement.

## How It Works
Network forensics relies on captured packet data (PCAPs) or flow data (NetFlow/IPFIX) collected at strategic network points — perimeter firewalls, internal switches, and endpoint network interfaces.

```
Network forensic data types:

Full Packet Capture (PCAP)
Complete record of every packet including payload content
Most detailed but storage-intensive
Captured with: Wireshark, tcpdump, commercial network taps
Allows reconstructing entire sessions, extracting transferred files,
reading unencrypted credentials, and replaying attack sequences
