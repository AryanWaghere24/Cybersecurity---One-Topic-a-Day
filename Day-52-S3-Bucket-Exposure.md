# Day 52 - S3 Bucket Exposure

## What It Is
S3 Bucket Exposure is one of the most common and damaging cloud security misconfigurations — when Amazon S3 (Simple Storage Service) buckets are accidentally made publicly accessible, exposing their contents to anyone on the internet. S3 buckets are used to store everything from website assets to database backups, customer data, source code, and internal documents. A single misconfigured bucket has been responsible for some of the largest data breaches in cloud history, exposing millions of records with no hacking required — just knowing the bucket's URL.

## How It Works
S3 buckets have multiple layers of access control — bucket policies, ACLs (Access Control Lists), and account-level Block Public Access settings. A misconfiguration at any layer can result in unintended public exposure.

```
S3 Access Control Layers:

1. Account-level Block Public Access (strongest protection)
AWS added this as a safeguard — when enabled, overrides all other settings
Should be enabled on every account that doesn't intentionally serve public content

2. Bucket Policy
JSON document defining who can access the bucket and what they can do
Misconfigured example — allows anyone to read all objects:
{
  "Effect": "Allow",
  "Principal": "*",        ← "*" means everyone on the internet
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::bucket-name/*"
}

3. Bucket ACL
Legacy access control — "public-read" ACL makes bucket contents world-readable

Common scenarios leading to exposure:
- Developer sets bucket to public for testing, forgets to revert
- Static website hosting enabled without realizing it makes bucket public
- Third-party tool or service requires public access, misconfigured scope
- Backup bucket created with same settings as public assets bucket
- Bucket name is guessable/predictable — attackers enumerate common names

How attackers find exposed buckets:
# GrayhatWarfare - search engine for public S3 buckets
https://buckets.grayhatwarfare.com

# AWS CLI - if you know the bucket name, test if it's public
aws s3 ls s3://target-bucket-name --no-sign-request

# Automated tools
pip install cloud-enum
cloud_enum -k companyname
# tries common bucket naming patterns: companyname-backup, companyname-dev, etc.
```

## Real-World Example
In 2017 Verizon suffered an S3 exposure where a third-party vendor (Nice Systems) stored call center data in a publicly accessible S3 bucket. The bucket contained names, addresses, phone numbers, and account PINs for approximately 14 million Verizon customers. The data was discovered by a security researcher using publicly available bucket scanning tools — no credentials, no exploitation, just an HTTP request to a public URL. The same year, Booz Allen Hamilton exposed classified US government data including credentials for government systems in a public S3 bucket. Both incidents required zero technical skill to discover — the data was simply sitting there, accessible to anyone who found the URL.

## Why It Matters
From an attacker's side, finding exposed S3 buckets requires no hacking skill whatsoever — automated tools enumerate buckets using common naming patterns (company-name-backup, company-name-dev, company-name-prod) and check if they're publicly accessible. Security researchers and attackers scan for these continuously. The data found often includes credentials that enable deeper access into the organization's cloud environment.

From a defender's side, AWS now enables Block Public Access by default on new accounts and buckets — but existing buckets and older accounts may still have this disabled. Regular auditing using tools like AWS Security Hub, Prowler, or ScoutSuite catches public buckets before attackers do. Every S3 bucket should have a documented reason for its access level, and any bucket not explicitly intended to be public should have Block Public Access enabled at both the bucket and account level.

## Key Terms
- S3 (Simple Storage Service): AWS's object storage service used to store files, backups, and data at scale
- Bucket Policy: a JSON document attached to an S3 bucket defining who can access it and what actions they can perform
- Block Public Access: an AWS account and bucket-level setting that prevents public access regardless of bucket policies or ACLs
- ACL (Access Control List): a legacy S3 access control mechanism — "public-read" ACL makes bucket contents world-readable
- Bucket Enumeration: automatically discovering S3 buckets by guessing common naming patterns and testing if they're publicly accessible

## One Tip / Tool

Tool: `cloud_enum` for bucket enumeration and `AWS CLI` for checking your own bucket configurations

```bash
# check if Block Public Access is enabled on your AWS account
aws s3control get-public-access-block --account-id YOUR_ACCOUNT_ID

# check Block Public Access settings on a specific bucket
aws s3api get-public-access-block --bucket your-bucket-name
