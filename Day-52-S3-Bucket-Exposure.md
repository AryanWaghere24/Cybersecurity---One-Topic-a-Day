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
