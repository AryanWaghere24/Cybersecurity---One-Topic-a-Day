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

3. Passing a role to a service
Required permissions: iam:PassRole + ec2:RunInstances (or similar)
Attacker launches an EC2 instance with an admin IAM role attached
SSHes into the instance and uses the instance's admin credentials
Result: admin access through the instance's metadata service

4. Updating an existing policy
Required permissions: iam:CreatePolicyVersion
Attacker adds administrator permissions to an existing policy they're attached to
Result: their existing permissions now include full admin access

5. Lambda privilege escalation
Required permissions: lambda:CreateFunction + iam:PassRole + lambda:InvokeFunction
Attacker creates a Lambda function with an admin role, invokes it to
execute arbitrary code with admin privileges

Real example attack chain:
Low-privilege user
→ has iam:PassRole + ec2:RunInstances
→ launches EC2 with AdminRole attached
→ SSHes in, queries metadata: curl http://169.254.169.254/latest/meta-data/iam/security-credentials/AdminRole
→ gets temporary admin credentials
→ full account compromise
```

## Real-World Example
In cloud penetration testing engagements, IAM privilege escalation is one of the most commonly found paths to full account compromise. Security researchers Spencer Gietzen and others at Rhino Security Labs documented over 20 distinct IAM privilege escalation techniques in AWS, demonstrating that many organizations unknowingly grant permission combinations that enable full admin access from what appear to be low-privilege starting points. In real breach investigations, attackers who gain initial access through SSRF (day 07), phishing (day 37-50), or exposed credentials routinely use IAM privilege escalation to expand from limited initial access to full cloud account control before exfiltrating data or deploying ransomware.
