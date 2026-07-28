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
