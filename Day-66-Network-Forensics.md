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

# Wireshark analysis on a PCAP file
# Key filters for incident response:

# Find all DNS queries (reveals C2 domain lookups)
# Wireshark filter: dns

# Find HTTP POST requests (data being sent out)
# Wireshark filter: http.request.method == "POST"

# Find large data transfers (potential exfiltration)
# Wireshark filter: tcp.len > 10000

# Follow a TCP stream to read full conversation
# Right click on packet → Follow → TCP Stream

# tshark - command line Wireshark for scripted analysis
# Extract all DNS queries from a PCAP
tshark -r capture.pcap -Y "dns.flags.response == 0" -T fields -e dns.qry.name

# Extract all HTTP hosts contacted
tshark -r capture.pcap -Y "http.request" -T fields -e http.host | sort -u

# Find all unique destination IPs
tshark -r capture.pcap -T fields -e ip.dst | sort -u

# NetworkMiner - extract files transferred over the network
# Automatically reconstructs files from PCAP
# Reveals: malware downloaded, documents exfiltrated, images transferred
```

Detecting specific attack patterns in network traffic:
```bash
# C2 beaconing detection (Cobalt Strike, day 27)
# Look for regular interval connections to same external IP
# tshark - find repeated connections to same destination
tshark -r capture.pcap -T fields -e ip.dst -e frame.time_delta \
  -Y "ip.dst == SUSPICIOUS_IP" | head -50
# Regular time deltas (e.g. every 60 seconds) = beaconing

# DNS tunneling detection (data exfiltration via DNS)
# Legitimate DNS queries are short — long subdomain queries indicate tunneling
tshark -r capture.pcap -Y "dns" -T fields -e dns.qry.name | \
  awk 'length > 50' | sort | uniq -c | sort -rn

# Lateral movement detection (SMB/WinRM across internal network)
tshark -r capture.pcap -Y "smb || smb2" -T fields \
  -e ip.src -e ip.dst -e smb.cmd | sort -u

# Data exfiltration detection (large outbound transfers)
tshark -r capture.pcap -Y "ip.dst != 192.168.0.0/16" \
  -T fields -e ip.dst -e tcp.len | \
  awk '{sum[$1]+=$2} END {for(ip in sum) print sum[ip], ip}' | sort -rn
```
## Real-World Example
During the investigation of the 2014 Sony Pictures breach, network forensics played a crucial role in understanding the scope of data exfiltration. Network traffic analysis revealed that attackers had exfiltrated terabytes of data — unreleased films, scripts, executive emails, and employee personal information — using standard HTTP and FTP connections that blended in with normal traffic. The network forensic analysis identified the specific external IPs data was sent to, the timing and volume of transfers, and the internal systems that participated in the exfiltration. This network evidence, combined with disk and log forensics, provided a complete picture of one of the most damaging corporate data breaches in history.
