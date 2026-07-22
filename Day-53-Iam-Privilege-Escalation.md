# Day 53 - IAM Privilege Escalation

## What It Is
IAM Privilege Escalation in cloud environments is the process of exploiting misconfigured Identity and Access Management permissions to gain more access than originally granted — ultimately aiming for full administrator control over a cloud account. It's the cloud equivalent of Linux privilege escalation (day 08), but instead of exploiting SUID binaries or sudo misconfigurations, attackers exploit overly permissive IAM policies, misconfigured roles, and unintended permission combinations. A single IAM misconfiguration can allow a low-privilege attacker to elevate to full cloud account administrator.

## How It Works
AWS IAM controls everything in a cloud account — who can launch servers, access databases, read secrets, and manage billing. When IAM policies are overly broad or misconfigured, attackers with limited initial access can chain together permissions to escalate to full admin.

```
Common IAM Privilege Escalation techniques:

1. Creating a new policy and attaching it to yourself
Required permissions: iam:CreatePolicyVersion or iam:AttachUserPolicy
Attacker creates an admin policy and attaches it to their own user
Result: instant administrator access

2. Assuming a more privileged role
Required permissions: sts:AssumeRole on a powerful role
If a low-privilege user can assume an admin role, they become admin
Result: full privileges of that role for the session duration
