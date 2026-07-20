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
