# Day 56 - Serverless Security

## What It Is
Serverless Security covers the unique attack surface introduced by serverless computing platforms — primarily AWS Lambda, Azure Functions, and Google Cloud Functions. In serverless architecture, developers write individual functions that run on demand without managing underlying servers. While serverless removes many traditional infrastructure security concerns, it introduces its own distinct attack vectors: over-privileged function permissions, insecure event triggers, function injection attacks, and ephemeral environment exploitation. Serverless functions are increasingly common in modern cloud applications, making understanding their security implications essential.

## How It Works
Serverless functions are triggered by events — HTTP requests, file uploads, database changes, message queue entries. Each function runs in an isolated ephemeral container that spins up, executes, and disappears. This architecture creates unique security characteristics.

```
Key serverless attack vectors:

1. Event Injection
Serverless functions often process untrusted input from event sources
If input isn't sanitized, classic injection attacks apply
SQL Injection (day 04) through API Gateway → Lambda → RDS
Command injection in Lambda functions processing user-supplied data

Example vulnerable Lambda function:
import subprocess
def handler(event, context):
    filename = event['filename']  # attacker controlled
    result = subprocess.run(f'cat {filename}', shell=True)  # command injection
    return result

2. Over-Privileged Lambda Roles
Lambda functions need IAM roles to access other AWS services
Common mistake: attaching AdministratorAccess to a Lambda function
If the function is compromised, attacker inherits full admin permissions
Same IAM privilege escalation concepts from day 53 apply here

3. Insecure Dependencies
Lambda functions package their own dependencies (node_modules, pip packages)
Vulnerable or malicious packages in the deployment package
Supply chain attacks targeting commonly used serverless frameworks

5. Denial of Wallet (DoW)
Unlike traditional DoS (Denial of Service), serverless scales automatically
Attacker triggers massive numbers of function invocations
AWS bills for every invocation and compute millisecond
Malicious traffic can generate enormous unexpected cloud bills

4. Environment Variable Secrets
Secrets stored as Lambda environment variables
Visible in plaintext in AWS console and deployment configurations
If function code is compromised, environment variables are accessible

6. Cold Start Information Leakage
Ephemeral containers sometimes reuse execution environments
Data left in /tmp or memory from previous invocations
Can leak sensitive data between function executions
```

## Real-World Example
In 2019 security researchers discovered that a popular serverless application framework had a vulnerability allowing attackers to read environment variables from Lambda functions through a carefully crafted event payload. Since many developers store database credentials, API keys, and other secrets as Lambda environment variables (a common but insecure practice), this vulnerability potentially exposed secrets across thousands of Lambda deployments using the affected framework. The incident highlighted how the abstraction of serverless doesn't eliminate security risks — it moves them to different layers like function code, dependencies, and configuration.

## Why It Matters
From an attacker's side, serverless functions expand the attack surface of web applications — every Lambda function reachable through an API Gateway is a potential target for injection attacks, and over-privileged functions provide paths to broader AWS account access. The ephemeral nature makes forensic investigation harder.
