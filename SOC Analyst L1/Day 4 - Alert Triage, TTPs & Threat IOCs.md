# TTPs (Tactics, Techniques and, Procedures) in SOC

TTPs stands for:

- **T** → Tactics
- **T** → Techniques
- **P** → Procedures

TTPs describes how attackers think, act, and operates during cyber attack

## Tactics in TTPs

Tactic is the attacker’s high-level goal or objective during an attack.

*“What the attacker is trying to achieve.”*


## Techniques in TTPs

A Technique is the method or approach attackers use to achieve their objective (tactic) during a cyberattack.

*“How the attacker performs the attack.”*


## Procedures in TTPs

A Procedure is the specific step-by-step implementation or exact way an attacker uses a technique or tools uses during an attack.

*“Exactly how the attacker performed the attack.”*


|Term|Meaning|
|---|---|
|Tactic|What attacker wants|
|Technique|How attacker attacks|
|Procedure|Exact steps/tools used|

### SOC Analyst use TTPs to:

- Detect attacks even when IOCs change
- Understand attackers intent
- Build better detections, alerts, and response playbooks

# IOC (Indicator of Compromise)

An IOC is a piece of evidence that indicates a system, network, or device may have been compromised by malicious activity.

*If an IOC tell you what happened,*
*TTPs tell you how and why it happened.*

IOC = "Something bad happened here, and we can prove it with data."

That "data" comes from: 
- Logs
- Network Traffic
- Endpoint activity
- Email headers
- File systems

### In a real SOC environment, IOCs help you:

- Trigger alerts in SIEM
- Confirm malicious activity
- Correlate attacks across systems
- Respond quickly to incidents
- Write incident reports
- Identify compromised systems
- Detect malware infections
- Block malicious IPs/domains
- Perform threat hunting
- Investigate security incidents

# Types of IOCs (Indicators of Compromise)

## 1. Network-Based IOCs

- Malicious IP addresses
- Suspicious domains
- DNS anomalies
- Unusual network traffic
- C2 server communication
- Suspicious URLs

## 2. Host-Based IOCs

- Unknown processes
- Suspicious registry changes
- New admin accounts
- Unauthorized scheduled tasks
- Abnormal system behavior
- File integrity changes

## 3. File-Based IOCs

- Malicious file hashes
- Suspicious filenames
- Malware signatures
- Infected executables
- Modified system files