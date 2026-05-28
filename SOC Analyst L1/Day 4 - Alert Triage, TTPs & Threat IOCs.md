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

## 4. E-mail Based IOCs

- Suspicious sender email addresses
- Spoofed domains
- Malicious attachments
- Phishing links
- Fake login pages
- Suspicious email headers
- Urgent or threatening language
- Shortened/masked URLs
- Unusual reply-to addresses
- Embedded malware files

# IOC Confidence Levels

IOC Confidence Level indicates how trustworthy, reliable, or accurate an Indicator of Compromise (IOC) is.

It helps SOC analysts determine:

- whether an IOC is truly malicious,
- suspicious,
- or possibly a false positive.


|Confidence Level|Meaning|Good Example|SOC Analyst Action|
|---|---|---|---|
|Low|Weak evidence, may be false positive|Single suspicious IP connection|Monitor activity and validate with logs|
|Medium|Suspicious IOC with some malicious indicators|Known phishing domain detected in email|Investigate user activity and correlate alerts|
|High|Strong evidence of compromise|Malware hash detected with active execution on endpoint|Isolate endpoint and escalate incident|
|Very High|Multiple confirmed malicious indicators correlated together|Malware hash + C2 communication + privilege escalation detected|Immediate containment, block IOCs, initiate incident response|
*SOC analyst never rely on single IOC*

# IOC -> Alerts -> Investigation (Real SOC Flow)

1. IOC detect (IP /  hash / process)
2. SEIM generates alert
3. SOC L1 validates IOC
4. SOC maps to TTP
5. Decision: True Positive or False Positive
6. Escalation or Closure

# Alert Triage

Alert Triage is the process of analyzing, prioritizing, and validating security alerts to determine:

- whether the alert is real or false positive,
- how severe it is,
- and what action should be taken.

```
Alert Comes → Analyze → Prioritize → Respond
```

Triage decides whether an alert becomes an incident


# Alert Prioritisation

Alert Prioritisation is the process of ranking security alerts based on their severity, risk, and impact so SOC analysts can respond to the most critical threats first.

## Alert Prioritisation Process

### 1. Filter the Alerts

- Avoid duplicate alerts
- Ignore already investigated alerts
- Focus on new and unresolved alerts
- Remove false positives

### 2. Sort by Severity

Start investigating:

```
Critical → High → Medium → Low
```

Critical alerts usually indicate:

- Active attacks
- Malware execution
- Ransomware activity
- Privilege escalation

### 3. Sort by Time

- Investigate oldest alerts first
- Older alerts may indicate ongoing compromise
- Delayed response can increase damage

Tryhackme Lab:- https://tryhackme.com/room/socl1alerttriage

