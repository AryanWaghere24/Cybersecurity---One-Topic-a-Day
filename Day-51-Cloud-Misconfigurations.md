# Day 51 - Cloud Misconfigurations

## What It Is
Cloud Misconfigurations are security weaknesses caused by incorrect, insecure, or overly permissive settings in cloud infrastructure — AWS, Azure, Google Cloud, and others. Unlike traditional attacks that exploit software vulnerabilities, misconfiguration attacks exploit human error in how cloud services are set up. A single misconfigured S3 bucket, an overly permissive IAM role, or an exposed management port can hand attackers access to terabytes of sensitive data or full cloud account control. Misconfiguration is consistently the leading cause of cloud data breaches according to every major cloud security report.

## How It Works
Cloud platforms offer hundreds of services with thousands of configuration options. The default settings are often insecure, and the complexity of cloud environments means misconfigurations are easy to introduce and hard to detect manually.

```
Most common cloud misconfiguration categories:

1. Public Storage Buckets
S3 buckets, Azure Blob containers, GCP Storage buckets set to public
Anyone on the internet can read (or write) the contents
Common data exposed: customer PII, credentials, backups, source code

2. Overly Permissive IAM Policies
Identity and Access Management roles with more permissions than needed
"AdministratorAccess" given to a role that only needs to read one S3 bucket
If that role is compromised, attacker has full account control

3. Exposed Management Interfaces
RDP (port 3389), SSH (port 22), database ports open to 0.0.0.0/0
Security groups allowing inbound traffic from "anywhere" instead of specific IPs

4. Disabled Logging and Monitoring
CloudTrail, Azure Monitor, GCP Cloud Audit Logs turned off
Attackers can operate for months without leaving any detectable trace

5. Hardcoded Credentials in Code
AWS access keys committed to public GitHub repositories
Attackers scan GitHub continuously for exposed cloud credentials
Automated tools find and abuse these within minutes of being pushed
```

Example of a misconfigured S3 bucket policy:
```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::company-backups/*"
}
```

The `"Principal": "*"` means anyone on the internet can read every file in this bucket.

## Real-World Example
The 2019 Capital One breach (also referenced in day 07 for SSRF) combined both SSRF and misconfiguration. The SSRF vulnerability allowed the attacker to reach the AWS metadata service, but it was an overly permissive IAM role attached to the web server that made the breach catastrophic. The server's IAM role had excessive S3 permissions — it could list and download from over 700 S3 buckets. A properly scoped IAM role would have limited what the attacker could access even after successfully exploiting the SSRF vulnerability. The misconfiguration turned a serious vulnerability into a 100-million-record breach.

## Why It Matters
From an attacker's side, scanning for cloud misconfigurations is largely automated and passive — tools continuously scan the internet for public S3 buckets, exposed databases, and leaked credentials on GitHub. No active exploitation of vulnerabilities is required. Many significant breaches happen because an attacker simply found something that was left open.

From a defender's side, Cloud Security Posture Management (CSPM) tools continuously scan cloud environments for misconfigurations and alert on violations of security best practices. AWS provides native tools like Security Hub, Trusted Advisor, and Config Rules. The principle of least privilege applied to IAM is the single most impactful control — every role, user, and service should have only the minimum permissions needed to function.

## Key Terms
- Cloud Misconfiguration: an insecure or incorrect setting in cloud infrastructure that exposes resources to unauthorized access
- IAM (Identity and Access Management): the system controlling who can access what in a cloud environment — users, roles, and policies
- Security Group: a virtual firewall in AWS controlling inbound and outbound traffic to cloud resources
- CSPM (Cloud Security Posture Management): tools that continuously monitor cloud environments for misconfigurations and compliance violations
- Least Privilege: the security principle that every user, role, and service should have only the minimum permissions necessary to perform its function

## One Tip / Tool

Tool: `ScoutSuite` and `Prowler` — open source cloud security auditing tools

```bash
# Prowler - comprehensive AWS security assessment tool
pip install prowler
prowler aws
