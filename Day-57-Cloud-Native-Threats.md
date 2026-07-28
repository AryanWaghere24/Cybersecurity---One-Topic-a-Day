# Day 57 - Cloud Native Threats (CSPM & CWPP)

## What It Is
Cloud Native Threats refers to the category of security risks unique to modern cloud-native architectures — and CSPM (Cloud Security Posture Management) and CWPP (Cloud Workload Protection Platform) are the two primary defensive tool categories built specifically to address them. CSPM continuously monitors cloud configurations for misconfigurations and compliance violations (the kinds covered in days 51-54), while CWPP protects the runtime workloads themselves — containers, virtual machines, and serverless functions — against active threats. Together they represent the defensive layer purpose-built for cloud environments that traditional on-premise security tools weren't designed to handle.

## How It Works
Cloud native environments are dynamic — infrastructure spins up and down automatically, configurations change constantly, and the attack surface shifts continuously. Traditional security tools designed for static on-premise environments can't keep up.

```
CSPM (Cloud Security Posture Management):

What it does:
- Continuously scans cloud configurations across AWS, Azure, GCP
- Detects misconfigurations in real time (public S3 buckets, open security groups)
- Maps configurations against compliance frameworks (CIS, SOC2, PCI-DSS, HIPAA)
- Prioritizes findings by risk severity
- Provides remediation guidance and sometimes auto-remediation

What CSPM catches:
✓ Public S3 buckets (day 52)
✓ Overly permissive IAM roles (day 53)
✓ Exposed management ports (SSH/RDP open to 0.0.0.0/0)
✓ Disabled CloudTrail logging
✓ Unencrypted storage volumes
✓ Missing MFA on root accounts
✓ Containers running as root (day 55)

CWPP (Cloud Workload Protection Platform):

What it does:
- Protects running workloads at runtime — VMs, containers, serverless
- Detects active threats: malware, cryptominers, lateral movement
- Behavioral monitoring: flags unusual process execution, network connections
- Vulnerability scanning of running workloads
- Container runtime security (detects escape attempts, day 55)

What CWPP catches:
✓ Cryptomining malware deployed on compromised instances
✓ Reverse shells spawned from web server processes (day 09)
✓ Container escape attempts (day 55)
✓ Lateral movement between cloud instances
✓ Unusual metadata service queries (day 54)
✓ Malicious process execution patterns
```

Attack patterns that CSPM + CWPP together detect:
```

Attack chain example:
1. SSRF vulnerability exploited (day 07)
   → CWPP detects unusual outbound request to 169.254.169.254
2. Metadata credentials stolen (day 54)
   → CSPM alerts on new API calls from unusual geographic location
3. IAM privilege escalation attempted (day 53)
   → CSPM detects policy attachment outside normal patterns
4. Cryptominer deployed on EC2 instances
   → CWPP detects high CPU usage + known mining pool network connections
5. Data exfiltration from S3 (day 52)
   → CSPM/CWPP detects unusual S3 GetObject volume from new IP
```
## Real-World Example
After the Capital One breach in 2019 (referenced throughout days 07, 51, 54), cloud security teams across the industry significantly increased CSPM adoption. Capital One had the technical infrastructure to detect the attack but the misconfigured IAM role and SSRF combination created a gap. Modern CSPM tools would have flagged the overly permissive IAM role before it was exploited, and CWPP tools would have detected the unusual metadata service queries and subsequent S3 enumeration in real time — potentially stopping the breach before data exfiltration completed. The breach became a turning point for cloud native security tooling adoption across enterprise organizations.

## Why It Matters
From an attacker's side, understanding what CSPM and CWPP tools monitor helps in planning evasion — using slower, lower-volume data exfiltration to avoid anomaly detection thresholds, using living-off-the-land techniques in cloud environments (using legitimate AWS CLI commands rather than external tools), and targeting regions or accounts where logging is disabled.
