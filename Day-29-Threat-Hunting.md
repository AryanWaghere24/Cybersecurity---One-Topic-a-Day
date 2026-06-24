# Day 29 - Threat Hunting

## What It Is

Threat Hunting is the proactive process of searching for hidden threats that may have bypassed traditional security controls. Unlike SIEM alerts or antivirus detections, threat hunting assumes that an attacker may already be present in the environment and actively looks for evidence of compromise.

Rather than waiting for automated tools to generate alerts, threat hunters investigate suspicious behaviors, unusual patterns, and attacker techniques that may not yet have been detected by existing security controls.

## How It Works

Threat hunting typically starts with a hypothesis. A hunter uses knowledge of attacker tactics, threat intelligence, or unusual observations to guide an investigation. They then analyze logs, endpoint telemetry, network traffic, and other data sources to validate or reject that hypothesis.

```text
Common Threat Hunting Data Sources:

- Endpoint telemetry      - processes, command lines, registry activity
- Authentication logs     - login attempts, account activity
- Network traffic         - connections, DNS requests, data transfers
- SIEM events             - correlated security alerts
- EDR telemetry           - behavioral endpoint activity
- Threat intelligence     - attacker indicators and TTPs
```

Example hunting hypothesis:

```text
Hypothesis:
An attacker may be using PowerShell
for malicious activity while avoiding
existing detection rules.

Investigation:
Search for powershell.exe executions
containing encoded commands (-enc).

Result:
Three systems identified running
encoded PowerShell commands.

Conclusion:
Potential compromise discovered
before any alert was triggered.
```

Unlike traditional detection, threat hunting focuses on finding malicious behavior first and generating detections later.

## Real-World Example

One common threat hunting scenario involves attackers abusing PowerShell for post-exploitation activities. Because PowerShell is a legitimate Windows administration tool, many security controls allow it by default.

A threat hunter might search for PowerShell commands containing encoded payloads, unusual network connections, or execution from non-standard locations. During an investigation, they may discover multiple systems running the same encoded command and communicating with an external server.

Although no malware alert was generated, the combined evidence suggests attacker activity. The threat can then be investigated and contained before significant damage occurs.

Threat hunting is particularly effective against advanced attackers who use legitimate tools to blend into normal system activity.

## Why It Matters

From an attacker's perspective, avoiding detection often means using trusted tools and behaving similarly to legitimate users. These techniques can bypass signature-based detection systems and generate little or no alerts.

From a defender's perspective, relying solely on automated detections creates blind spots. Threat hunting helps uncover unknown threats, validate security assumptions, and identify weaknesses in existing detection coverage.

Modern Security Operations Centers (SOCs) perform threat hunting regularly to reduce attacker dwell time and improve overall security visibility.

## Key Terms

* Threat Hunting: proactive searching for hidden malicious activity within an environment.
* Hypothesis-Based Hunting: investigating a theory about possible attacker behavior.
* IOC (Indicator of Compromise): evidence suggesting a system may be compromised.
* TTPs (Tactics, Techniques, and Procedures): methods attackers use during an intrusion.
* Dwell Time: the amount of time an attacker remains undetected.
* Threat Intelligence: information about known attackers, techniques, and indicators.
* Living off the Land: abusing legitimate system tools for malicious purposes.

## One Tip / Tool

Tool: `Velociraptor`

Velociraptor is a powerful open-source endpoint visibility and threat hunting platform that allows investigators to collect forensic data, search systems, and identify suspicious activity across multiple endpoints.

```text
Example Hunt:

Process Name:
powershell.exe

Command Line Contains:
-enc

Purpose:
Identify potentially malicious
encoded PowerShell commands
commonly used during post-exploitation.
```

Free hands-on practice — The Threat Hunter Playbook and MITRE ATT&CK provide excellent resources for learning real-world hunting methodologies and understanding how attackers operate inside enterprise environments.
