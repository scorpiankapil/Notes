# Cyber Kill Chain Methodology

The Cyber Kill Chain is a cybersecurity model used to identify and understand the stages of a cyberattack. It was created by Lockheed Martin

How cyber attacks happen step-by-step.

It is a linear model that focuses on the attacker's journey from the outside in. By breaking the chain at any point, you stop the entire attack.


## 7 Stages of Cyber Kill Chain

| Stage                  | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| Reconnaissance         | Attacker gathers information about target             |
| Weaponization          | Malicious payload/exploit is prepared                 |
| Delivery               | Malware or payload delivered to victim                |
| Exploitation           | Exploiting the Vulnerability                          |
| Installation           | Malware installed on system                           |
| Command & Control (C2) | Attacker communicates with compromised system         |
| Actions on Objectives  | Data theft, ransomware, destruction, launch DDoS etc. |

| Phase                         | Description                                                                                             | Common Ethical Hacking Activity                                |
| ----------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **1. Reconnaissance**         | Gathering information about the target (OSINT, scanning, enumeration).                                  | Passive & Active Footprinting                                  |
| **2. Weaponization**          | Creating a malicious payload by combining an exploit with malware or a backdoor.                        | Payload creation using Metasploit, Cobalt Strike               |
| **3. Delivery**               | Sending the malicious payload to the target through a delivery method.                                  | Phishing emails, malicious websites, USB attacks               |
| **4. Exploitation**           | Exploiting a vulnerability to execute the payload on the victim's system.                               | SQL Injection, Buffer Overflow, RCE                            |
| **5. Installation**           | Installing malware or a backdoor to maintain access to the compromised system.                          | Installing RATs, Backdoors, Rootkits                           |
| **6. Command & Control (C2)** | Establishing communication between the attacker's server and the compromised system for remote control. | Configuring C2 frameworks (e.g., Cobalt Strike, Metasploit)    |
| **7. Actions on Objectives**  | Achieving the attacker's goal such as data theft, ransomware deployment, or system destruction.         | Data exfiltration, Privilege Escalation, Ransomware simulation |

## 1. Reconnaissance

Reconnaissance is the first phase of the Cyber Kill Chain where the attacker collects information about the target before launching an attack. The goal is to identify potential weaknesses and understand the target's infrastructure.

- Reconnaissance is the process of gathering information about a target before attacking it.

- Collecting public information (OSINT)
- Finding IP addresses and domains
- DNS enumeration
- Port scanning
- Service identification
- Employee information gathering

**Example**

An attacker searches the company's website, LinkedIn profiles, and performs an Nmap scan to identify open ports.

## 2. Weaponization

Weaponization is the phase where the attacker creates a malicious payload by combining an exploit with malware or a backdoor. This payload is prepared to exploit the target's vulnerability.

- Weaponization is the process of creating a malicious payload to attack the target.

- Creating malware
- Generating payloads
- Embedding malicious code in documents
- Preparing exploits

**Example**

An attacker creates a malicious PDF containing a backdoor using Metasploit.

## 3. Delivery

Delivery is the phase where the attacker sends the malicious payload to the target using different attack methods.

- Delivery is the process of sending the malicious payload to the victim.

- Phishing emails
- Malicious websites
- USB devices
- Social engineering
- Drive-by downloads

**Example**

The attacker emails the malicious PDF to an employee pretending to be from the HR department.

## 4. Exploitation

Exploitation is the phase where the attacker takes advantage of a vulnerability to execute the malicious payload on the victim's system.

- Exploitation is the process of using a vulnerability to gain unauthorized access or execute malicious code.

- SQL Injection
- Buffer Overflow
- Remote Code Execution (RCE)
- Cross-Site Scripting (XSS)
- Privilege Escalation

**Example**

The employee opens the malicious PDF, and the embedded exploit executes the malware.

## 5. Installation

Installation is the phase where the attacker installs malware or a backdoor on the compromised system to maintain access.

- Installation is the process of installing malicious software on the victim's system.

- Installing a Remote Access Trojan (RAT)
- Creating backdoors
- Installing rootkits
- Creating persistence mechanisms

**Example**

The malware installs itself and creates a startup entry so it runs every time the computer boots.

## 6. Command and Control (C2)

Command and Control (C2) is the phase where the compromised system establishes a communication channel with the attacker's server. This allows the attacker to remotely control the infected system.

- Command and Control (C2) is a communication channel that allows attackers to remotely control a compromised system.

- Connecting to a C2 server
- Receiving attacker commands
- Sending stolen data
- Downloading additional malware

**Example**

The infected computer connects to the attacker's C2 server and waits for instructions.

## 7. Actions on Objectives

This is the final phase where the attacker performs their intended objective after successfully compromising the target.

- Actions on Objectives is the phase where the attacker achieves the goal of the cyberattack.

- Data theft
- Data exfiltration
- Ransomware deployment
- Destroying data
- Encrypting files
- Spying on users

 **Example**

The attacker steals customer data, encrypts company files with ransomware, or deletes important business data.


# Standard Hacking Methodology

Standard Hacking Methodology is a structured step-by-step process followed by ethical hackers and attackers to identify, exploit, and assess security weaknesses in a system or network.

It provides a systematic approach to conducting security assessments or cyberattacks.

| Phase                  | Purpose                                                        |
| ---------------------- | -------------------------------------------------------------- |
| **Reconnaissance**     | Gather information about the target                            |
| **Scanning**           | Identify live hosts, open ports, services, and vulnerabilities |
| **Gaining Access**     | Exploit vulnerabilities to access the target                   |
| **Maintaining Access** | Maintain persistent access to the compromised system           |
| **Clearing Tracks**    | Remove evidence of the attack to avoid detection               |

# Alert Reporting (Documentation)

Alert reporting is the process of recording, documenting, and notifying security teams about suspicious activities or security incidents detected by security tools such as SIEM, IDS/IPS, EDR, antivirus, or firewalls.

- **Who**: Which user logs in, runs the command, or downloads the file
- **What**: What exact action or event sequence was performed
- **When**: When exactly did the suspicious activity start and ended
- **Where**: Which device, IP, or website was involved in the alert
- **Why**: The most important W, the reasoning for your final verdict

## Why Alert Reporting Matters

- **Early Threat Detection**  
    Helps identify suspicious or malicious activities before they become major security incidents.
- **Faster Incident Response**  
    Notifies SOC analysts immediately so they can investigate and respond quickly.
- **Prioritizes Critical Threats**  
    Classifies alerts by severity (Low, Medium, High, Critical) to focus on the most serious incidents first.
- **Reduces Security Risks**  
    Enables quick action to minimize damage, data loss, and service disruption.
- **Supports Incident Investigation**  
    Provides detailed information such as timestamps, IP addresses, and event logs for forensic analysis.
- **Improves Security Monitoring**  
    Gives continuous visibility into network and system activities.
- **Helps Meet Compliance Requirements**  
    Maintains records of security events for audits and regulatory compliance (e.g., PCI DSS, HIPAA, ISO 27001).
- **Identifies Attack Patterns**  
    Helps SOC teams recognize recurring attacks and improve detection rules.
- **Enhances Decision-Making**  
    Provides accurate information for security teams to make informed response decisions.
- **Strengthens Overall Security**  
    Helps organizations continuously improve their security posture by learning from past incidents.

### Example: Tier-1 Alert Report (Short)

**Summary:**  
PowerShell executed with an encoded command triggered by a Microsoft Word document on a finance user's system.

**Analysis:**  
The execution occurred outside business hours. The parent process was **winword.exe**, and an external network connection was observed.

**Verdict:**  
**True Positive** – Suspicious PowerShell execution.

**Recommendation:**  
Escalate the incident to **SOC L2** for containment and further investigation.

### Example 2: Tier-1 Alert Report (Short)

**Summary:**

Multiple failed login attempts followed by a successful login from an unknown external IP address on the HR manager's account.

**Analysis:**

More than 30 failed login attempts were detected within 5 minutes. The successful login originated from an unfamiliar IP address in another country, outside normal business hours. The user confirmed they did not attempt the login.

**Verdict:**

True Positive – Suspected brute-force attack leading to account compromise.

**Recommendation:**

Reset the user's password, enable MFA, block the malicious IP address, and escalate the incident to **SOC L2** for further investigation.

# What is Escalation?

Escalation in SOC is the process of forwarding a security alert or incident to a higher-level analyst or another team when it requires more expertise, authority, or immediate action.

- Ensures serious threats are handled quickly.
- Involves experienced analysts for complex incidents.
- Reduces the impact of cyber attacks.
- Improves incident response efficiency.

## When Should Tier-1 Escalate?

|Condition|Explanation|Example|
|---|---|---|
|**Confirmed Malicious Activity**|The analyst confirms that the activity is a real cyberattack.|Malware execution, ransomware detected|
|**Privileged Account Involved**|The attack involves a high-privilege account such as an Administrator or Domain Admin.|Admin user account compromised|
|**Critical Asset Affected**|The affected system is critical to the organization.|Domain Controller (DC), Database Server, Email Server|
|**Multiple Alerts Correlated**|Several related alerts indicate an ongoing attack instead of a single event.|Phishing email → PowerShell execution → C2 connection|
|**Data Risk Exists**|There is a possibility that sensitive data has been stolen, modified, or leaked.|Possible data exfiltration or database access|
|**Policy Requires Escalation**|The organization's SOC policy requires escalation based on severity or asset type.|High or Critical severity alert|
**Escalation is not failure, It's professionalism**

# What is SOC Communication

SOC Communication is the process of sharing security-related information between SOC analysts, IT teams, incident response teams, management, and other stakeholders to ensure effective detection, investigation, and response to cyber threats.

| Team                           | Purpose                                        |
| ------------------------------ | ---------------------------------------------- |
| SOC L1 ↔ SOC L2                | Escalate and investigate incidents             |
| SOC ↔ Incident Response Team   | Containment and recovery                       |
| SOC ↔ IT Team                  | Patch systems and resolve issues               |
| SOC ↔ Management               | Incident status and business impact            |
| SOC ↔ Threat Intelligence Team | Share threat indicators and attack information |