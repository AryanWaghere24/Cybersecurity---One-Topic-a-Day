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
