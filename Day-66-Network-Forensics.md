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

NetFlow / IPFIX (Flow Data)
Metadata only — source IP, destination IP, port, bytes, duration
No payload content — cannot read data but shows communication patterns
Much lower storage requirements than full PCAP
Useful for: detecting lateral movement, identifying C2 beaconing patterns,
finding data exfiltration by volume

DNS Logs
Every domain name lookup made on the network
Reveals: C2 domain lookups, DGA activity (day 27 Cobalt Strike),
data exfiltration via DNS tunneling, phishing domain visits

Firewall and Proxy Logs
Allowed and blocked connections with timestamps
URL categories and reputation scores
Identifies: connections to known malicious IPs (IOCs, day 60),
policy violations, unusual ports and protocols
```

Key network forensic analysis techniques:
```bash
# tcpdump - capture network traffic from command line
tcpdump -i eth0 -w capture.pcap              # capture all traffic
tcpdump -i eth0 -w capture.pcap port 80      # capture only HTTP
tcpdump -i eth0 -w capture.pcap host 192.168.1.10  # capture specific host
