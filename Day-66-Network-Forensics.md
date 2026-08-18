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

## Why It Matters
From an attacker's side, network traffic is increasingly encrypted — HTTPS, TLS-encrypted C2, and DNS over HTTPS all limit what network forensics can see in terms of content. However, traffic metadata (who talked to whom, when, how much data) remains visible and reveals patterns even without payload visibility.

From a defender's side, network forensics provides the only view of cross-system attacker activity — disk and memory forensics show what happened on individual machines, but network forensics shows how attackers moved between systems, what data left the organization, and what external infrastructure they used. Deploying network capture at key chokepoints (internet gateway, internal segment boundaries) and retaining NetFlow data for 90+ days provides the visibility needed for thorough incident investigation.

## Key Terms
- Network Forensics: capturing and analyzing network traffic to investigate security incidents and reconstruct attacker communications
- PCAP (Packet Capture): a file format storing captured network packets including full payload content — the primary artifact in network forensics
- NetFlow: network traffic metadata (no payload) showing communication patterns between hosts — lower storage cost than full PCAP
- C2 Beaconing: the regular check-in pattern of malware communicating with its command and control server — detectable as regular interval connections
- DNS Tunneling: encoding data within DNS queries to exfiltrate information or establish C2 channels through firewalls that allow DNS traffic

## One Tip / Tool

Tool: `Wireshark` for interactive analysis and `Zeek` (formerly Bro) for automated network security monitoring

```bash
# Zeek - open source network analysis framework
# Converts raw network traffic into structured logs automatically
apt install zeek

# Run Zeek against a PCAP file
zeek -r capture.pcap

# Zeek automatically generates logs:
# conn.log     - all network connections
# dns.log      - all DNS queries and responses
# http.log     - all HTTP requests
# ssl.log      - SSL/TLS certificate information
# files.log    - files transferred over the network
# weird.log    - unusual or suspicious network behavior

# Query Zeek logs for C2 beaconing
cat conn.log | zeek-cut id.orig_h id.resp_h duration | \
  awk '$3 < 1' | sort | uniq -c | sort -rn | head -20

# RITA (Real Intelligence Threat Analytics)
# Built on top of Zeek - automatically detects beaconing, DNS tunneling,
# long connections, and other C2 indicators
git clone https://github.com/activecm/rita
# RITA analyzes Zeek logs and scores each connection for likelihood of being C2

# Practical Wireshark display filters for incident response:
# All traffic to/from a suspicious IP
ip.addr == SUSPICIOUS_IP
# All DNS queries
dns.flags.response == 0
# Failed TCP connections (scanning, connection refused)
tcp.flags.reset == 1
# Large packets (possible data exfiltration)
frame.len > 1400
```

Network forensics is most powerful when combined with the other forensic disciplines covered in this category — a complete incident investigation correlates network traffic (what left the network and when), memory forensics (what was running at the time), disk forensics (what files and logs exist), and log forensics (what the audit trail shows) into a single unified timeline of the entire attack from initial compromise through to final objective. No single data source tells the complete story — all four together do.
