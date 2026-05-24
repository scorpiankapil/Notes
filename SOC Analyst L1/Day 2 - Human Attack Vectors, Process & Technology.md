The main focus of SOC team is to keep Detection and Response intact.
People, process, and Technology coexist in the SOC environment. A team of professional individuals working on state-of-the-art security tools in the presence of proper processes is what makes a mature SOC environment.

* CISO
    * SOC Manager
        * SOC Analyst (Level 1)
        * SOC Analyst (Level 2)
        * SOC Analyst (Level 3)
        * Security Manager
        * Detection Engineer


## People
**SOC Analyst (Level 1)**  
Handles continuous monitoring of security tools like SIEM, IDS/IPS, and EDR. Filters false positives, identifies suspicious activity, and escalates real incidents using defined procedures.

**SOC Analyst (Level 2)**  
Takes ownership of confirmed alerts and performs deep investigation and analysis. Uses threat intelligence, log correlation, and forensics to contain and remediate incidents.

**SOC Analyst (Level 3)**  
Works on advanced threat hunting and complex attack scenarios (APTs). Improves SOC processes, detection logic, and provides technical guidance to junior analysts.

**Security Manager**  
Manages the SOC team, defines security policies, and ensures compliance and risk management. Acts as a bridge between technical teams and business leadership.

**Detection Engineer**  
Creates, tests, and tunes detection rules in SIEM and EDR platforms. Focuses on proactive detection, automation, and reducing alert fatigue with high-quality alerts.


## Process
**Alert Triage**
The alert triage is the basis of the SOC team. The first response to any alert is to perform the triage

**5 Ws**
1. What?
A malicious file was created on one of the hosts inside the organization's newtowk.

2. When?
The file was detected at 13:30 on June 5, 2025.

3. Where?
The file was detected in the directory of the host: "GEORGE PC".

4. Who?
The file was detected for the user George.

5. Why?
After the investigation, it was found that the file was downloaded from a pirated software-selling website. The investigation with the user revealed that they downloaded the file as they wanted to use a software for free.

# Reporting
The detected harmful alerts need to be escalated to higher-level analyst for a timely response and resolution. These alerts are escalated as tickets and assigned to the relevant people. The report should discuss all the 5 Ws along with a through analysis, and screenshots should be used as evidence of the activity. 

## Incident Response and Forensics
Sometimes, the reported detections point to highly malicious activities that are critical. In these scenarios, high-level teams initiate an incident response.

A few times, a detailed forensics activity also needs to be performed. This forensics activity to determine the incident's root cause.

## Technology
Having the right **People** and **Processes** in place would never be enough without security solutions for detection and response. The **Technology** portion in the SOC pillars refers to the security solutions. These security solutions efficiently minimize the SOC team’s manual effort to detect and respond to threats.

Let’s get a brief understanding of some of these security solutions:

**SIEM:**  
Security Information and Event Management (SIEM) is a popular tool used in almost every SOC environment. This tool collects logs from various network devices, referred to as log sources.

Detection rules are configured in the SIEM solution, which contain logic to identify suspicious activity. The SIEM solution provides detections after correlating data from multiple log sources and alerts us in case of a match with any of the rules.

Modern SIEM solutions go beyond rule-based detection analysis by providing user behavior analytics and threat intelligence capabilities. Machine learning algorithms support this to enhance detection capabilities.

**Note:** The SIEM solution only provides the Detection capabilities in a SOC environment.

---

**EDR:** 
Endpoint Detection and Response (EDR) provides the SOC team with detailed real-time and historical visibility of the devices’ activities. It operates on the endpoint level and can carry out automated responses. EDR has extensive detection capabilities for endpoints, allowing you to investigate them in detail and respond with a few clicks.

**Firewall:** A firewall functions purely for network security and acts as a barrier between your internal and external networks (such as the Internet). It monitors incoming and outgoing network traffic and filters any unauthorized traffic. The firewall also has some detection rules deployed, which help us identify and block suspicious traffic before it reaches the internal network.

Several other security solutions play unique roles in a SOC environment, such as Antivirus (Endpoint Protection Platform), IDS/IPS, XDR (Extended Detection and Response), SOAR (Security Orchestration, Automation, and Response), and more. The decision on what Technology to deploy in the SOC should be made after careful consideration of the threat surface and the available resources in the organization.

# Security Departments
In tiny companies, the IT department takes the role of securing the company. Small to medium-sized companies may have a generic “Information Security” team that does all sorts of tasks. Bigger companies have a CISO overseeing multiple security teams, each handling a specific task.

* ***Red Team:** Offensive security experts, pentesters, or ethical hackers who look for security issues.

* **GRC Team:** Specialists managing policies and ensuring compliance with regulations like PCI DSS.

* **Blue Team:** Defensive security experts like SOC analysts, engineers, or incident responders.

* **L1 Analysts:** Junior members who triage alerts and pass complex cases to L2.

* **L2 Analysts:** Experienced members who investigate more advanced attacks.

* **Engineers:** Experts in configuring security tools like EDR or SIEM.

* **Manager:** A person who manages the whole SOC team.

If SOC expertise is not enough or the incident goes out of control, you urgently call the CIRT (Cyber Incident Response Team), also called CSIRT or CERT. The members should have deep knowledge of cyber threats and handle breaches without depending on tools like EDR or SIEM.


# Human attacks vectors in SOC
Not every organization has the expertise to operate a SOC on its own and relies on a Managed Security Services Provider (MSSP), a company that delivers outsourced security services, most commonly SOC, to its clients. Working at MSSP is typically high-pressure, but it is also a good option to quick start your career.

## Why Humans Are Targeted
Humans are targeted because of the access they can provide - to websites, mailboxes, or databases. Some threat actors hunt for a specific access, while others are not so selective and just breach as many accounts as they can and decide how to use them later

Attacks targeting humans share a common trait: they rely on manipulating the victim into helping the attacker, whether knowingly or not. This tactic is known as social engineering, and it works by exploiting human psychology rather than technical flaws. For the tactic to succeed, it is designed to be:
* Trustworthy: The attacker must appear legitimate so the victim trusts them
* Emotional: The attack must trigger feelings like urgency, fear, or curiosity


## How Humans Are Targeted
● Phishing Attacks
● Malware Downloads
● Deep Fakes
● Impersonation
● Other Attacks like Keylogging, Physical attacks, etc

## How To Defend Humans
Defending against threats involves two key tasks: Mitigation and Detection. Mitigation aims to prevent or reduce the chance and impact of attacks, for example by training employees or deploying a good anti-phishing solution.

##### What PhishTank Is?
PhishTank is a community-driven anti-phishing platform — a website where people around the world help collect, verify, and share information about phishing attacks (fraudulent scam websites).
Link : https://www.phishtank.com/

## How To Defend Humans
As a SOC analyst, your task is to detect and investigate attacks, because after sometime you will be tired of manual mitigation & will want automated way and there comes the SOC suite of automated solutions. Some solutions are : 

● Anti-phishing solution
● Antivirus / EDR solution
● "Trust but verify" principle
● Security awareness training
