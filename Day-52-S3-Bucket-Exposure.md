# Day 52 - S3 Bucket Exposure

## What It Is
S3 Bucket Exposure is one of the most common and damaging cloud security misconfigurations — when Amazon S3 (Simple Storage Service) buckets are accidentally made publicly accessible, exposing their contents to anyone on the internet. S3 buckets are used to store everything from website assets to database backups, customer data, source code, and internal documents. A single misconfigured bucket has been responsible for some of the largest data breaches in cloud history, exposing millions of records with no hacking required — just knowing the bucket's URL.

## How It Works
S3 buckets have multiple layers of access control — bucket policies, ACLs (Access Control Lists), and account-level Block Public Access settings. A misconfiguration at any layer can result in unintended public exposure.
