# What is a Workbook in a SOC?

A **SOC Workbook** is an **interactive report/dashboard** that collects security data from different logs and presents it visually using **charts, tables, maps, and filters**.

- **Interactive:** Analysts can click/filter data to investigate specific events.
- **Real-time:** Can update as new log data arrives.
- **Data visualization:** Converts raw logs into charts, graphs, and tables.
- **Data consolidation:** Combines data from sources such as **firewalls, endpoints, Microsoft 365, and SIEM**.
- **Investigation:** Helps analysts identify suspicious patterns and investigate incidents.

#### Use Cases of Workbooks in SOC

|Use Case|How it is used|
|---|---|
|**Incident Overview**|Shows active alerts, severity, status, and assigned incidents in one dashboard.|
|**Threat Hunting**|Visualizes network and endpoint activity to identify suspicious patterns or attacker behavior.|
|**Failed Login Analysis**|Shows spikes in failed logins and helps identify possible brute-force attacks.|
|**Network Monitoring**|Displays traffic patterns, unusual connections, and communication with suspicious IPs/domains.|
|**Malware Investigation**|Correlates endpoint events, processes, files, and network connections to investigate malware.|
|**User Activity Monitoring**|Tracks unusual login locations, account activity, and privilege changes.|
|**Log Health Monitoring**|Shows whether servers and security devices are successfully sending logs to the SIEM.|
|**Alert Investigation**|Allows analysts to filter and drill down from a high-level alert into the underlying events.|

# SOC Lookup

A Lookup (often called a **Watchlist** in Sentinel) is essentially a **custom table of data** that you can **upload to a security platform to provide a extra context** that isn't found in standard logs.

- Raw logs often contain only basic information.
- A lookup adds **business or security context** to that data.
- Example: A log shows `192.168.1.5` accessed a file.
- The lookup can tell the SOC analyst that `192.168.1.5` belongs to the **CEO's laptop**.
- This helps analysts **prioritize and investigate alerts faster**.

#### Common Types

| Lookup Type             | Purpose                                                                  | Example                            |
| ----------------------- | ------------------------------------------------------------------------ | ---------------------------------- |
| **Asset Inventory**     | Maps IPs/hostnames to devices or owners.                                 | `10.0.0.5 → HR Database Server`    |
| **Threat Intelligence** | Contains known malicious IPs, domains, URLs, or file hashes.             | `X.X.X.X → Known malicious IP`     |
| **VIP List**            | Track high-value users such as executives or administrators.             | `admin@company.com → Domain Admin` |
| **Terminated Users**    | Contains accounts belonging to employees who have left the organization. | `user123 → Terminated employee`    |

# Assets in SOC

- **Asset:** Any physical or virtual resource that **stores, processes, or transmits data**.
- In a SOC, assets are tracked to understand **what could be affected during an attack**.

**Categories of Assets:**

| Type               | Simple Meaning                      | Examples                                |
| ------------------ | ----------------------------------- | --------------------------------------- |
| **Endpoint**       | User devices                        | Laptop, PC, mobile                      |
| **Infrastructure** | Systems that provide services       | Servers, VMs, containers, cloud systems |
| **Network Device** | Devices that manage network traffic | Router, switch, firewall, load balancer |
| **IoT/OT**         | Smart or industrial devices         | Cameras, printers, PLCs                 |

**Asset Context / Metadata**

|Metadata|Meaning|Example|
|---|---|---|
|**Criticality**|How important the asset is|Production database = High|
|**Ownership**|Who manages/uses it|IT Admin / Employee|
|**Patch Status**|Whether security updates are applied|Outdated OS = Risk|

# Identity in SOC

**Identity** = “Who is performing an action?”

An identity is a digital account/entity that has **permissions to access systems or resources**.

|Type|Simple Meaning|Example|
|---|---|---|
|**User Identity**|Human user account|Employee, contractor, guest|
|**Privileged Identity**|Account with high-level permissions|Domain Admin, Global Admin|
|**Service / Non-Human Identity**|Account used by applications or scripts|Backup service accessing a database|
|**Managed Identity**|Identity managed automatically by a cloud provider|Azure/AWS resource accessing another resource|

### Identity Perimeter

- Modern security focuses on **verifying identities**, not just trusting the physical network.
- Users can work remotely and access cloud applications from anywhere.
- Important controls include:
    - **MFA** → Requires multiple authentication factors.
    - **Conditional Access** → Allows/blocks access based on conditions such as device, location, risk, or user.

**SOC example:**  
If a **Domain Admin** suddenly logs in from an unusual location, the SOC investigates it with higher priority because the identity has **privileged access**.

---
# SOC Metrics

**SOC Metrics** are **measurable values used to evaluate how effectively a Security Operations Center (SOC) is working.**

Metrics = measurable values used to check how well a SOC is performing.

## SOC Metrics: MTTD, MTTA & MTTR

These three metrics measure **how quickly a SOC handles a security incident**.

|Metric|Full Form|Simple Meaning|Measures|
|---|---|---|---|
|**MTTD**|Mean Time to Detect|How long it takes to **detect a threat/incident**|Detection speed|
|**MTTA**|Mean Time to Acknowledge|How long it takes an analyst to **acknowledge an alert and start investigating**|Analyst response/acknowledgement speed|
|**MTTR**|Mean Time to Respond/Remediate|How long it takes to **respond to and contain/remediate the incident**|Resolution/response speed|

## MTTD — Mean Time to Detect

MTTD is the **measure of how long a threat exists in your environment** before security tools (SIEM, EDR, IDS) actually **trigger an alert.**

**Example:**

|Event|Time|
|---|--:|
|Hacker enters the network|Monday|
|SIEM/EDR detects the activity|Thursday|
|**MTTD**|**3 days**|

#### How can a SOC reduce MTTD?

- **Better log coverage** → Collect logs from more important systems.
- **Advanced analytics** → Detect unusual behavior and anomalies.
- **Threat Intelligence** → Quickly identify known malicious IPs, domains, and hashes.
- **Good SIEM/EDR monitoring** → Generate alerts quickly when suspicious activity occurs.

## MTTA — Mean Time to Acknowledge

MTTA is the **measure of how long it takes a SOC analyst to acknowledge an alert** after a security tool (SIEM, EDR, IDS) has triggered it.

**Example:**

|Event|Time|
|---|--:|
|SIEM generates an alert|10:00 AM|
|Analyst acknowledges the alert|10:05 AM|
|**MTTA**|**5 minutes**|

#### How to improve MTTA

- **Alert prioritization:** Critical alerts are handled first.
- **Automation:** Automatically assign or escalate important alerts.
- **Reduce alert fatigue:** Remove unnecessary/duplicate alerts.
- **24/7 monitoring:** Ensure alerts are reviewed promptly.

## MTTR — Mean Time to Respond / Remediate

**MTTR is the measure of how long it takes the SOC to respond to a security incident and take appropriate action to contain, resolve, or remediate the threat.**

**Example:**

Suppose an **EDR detects ransomware** on an employee's laptop.

|Time|Event|
|---|---|
|**10:00 AM**|Ransomware alert is generated|
|**10:05 AM**|SOC analyst starts investigating|
|**10:15 AM**|Analyst confirms ransomware infection|
|**10:20 AM**|Laptop is isolated from the network|
|**10:45 AM**|Malware is removed and system is restored|
|**MTTR**|**45 minutes**|

#### How to improve MTTR

- **Incident Response Playbooks:** Follow predefined steps for common incidents.
- **Automation:** Automatically isolate infected systems or block malicious IPs.
- **Clear Escalation:** Quickly involve the right security/IT teams.
- **Effective Tools:** Use SIEM, EDR, SOAR, and threat intelligence to speed up investigation and response.

## Efficiency & Quality Metrics

These metrics help a SOC determine **whether its security tools, alerts, and detection processes are actually working effectively.**

|Metric|Simple Definition|Example|
|---|---|---|
|**False Positive Rate**|Percentage of alerts that **look suspicious but are actually harmless**|1,000 alerts → 900 harmless → **90% false positives**|
|**True Positive Rate**|Percentage of alerts that **are actually real security incidents**|1,000 alerts → 100 real threats → **10% true positives**|
|**Alert Volume**|Total number of alerts generated by security tools|SIEM generates **10,000 alerts/day**|
|**Incident Volume**|Number of alerts that become confirmed security incidents|10,000 alerts → **100 actual incidents**|
|**Alert Volume vs. Incident Volume**|Compares total alerts with actual incidents to see how much **noise** the SOC receives|10,000 alerts but only 100 incidents → lots of noise|

## Strategic & Risk Metrics

These metrics help the SOC and **C-Suite (CEO, CISO, etc.)** understand the organization's overall security risk and whether the SOC is providing enough protection.

|Metric|Simple Definition|Example|
|---|---|---|
|**Dwell Time**|How long an attacker stays inside the environment **before being detected**|Attacker enters Monday → detected Thursday = **3 days**|
|**Coverage Mapping**|Measures how much of an attacker's techniques the SOC can **detect or monitor**|SOC can detect 80% of relevant MITRE ATT&CK techniques → **80% coverage**|
|**SLA Compliance**|Measures whether the SOC handles incidents **within the agreed time limit**|95% of critical alerts acknowledged within 15 min → **95% SLA compliance**|

#### 1. Dwell Time

**Dwell Time = Time between an attacker/infection entering the environment and the SOC detecting it.**

**Example:**

```
Attacker enters → Monday 10 AM  
SOC detects → Thursday 10 AM  
Dwell Time = 3 days
```


#### 2. Coverage Mapping — MITRE ATT&CK

**Coverage Mapping = Checking which attacker techniques your security tools and SOC can detect.**

A Percentage showing how much of the **"Attacker Playbook"** you can actually see. (e.g., "We have 80% coverage for Ransomware techniques").

**Example:**

```
MITRE ATT&CK has 100 relevant techniques.  
Your SOC can effectively detect 80.  
Coverage = 80%
```

It helps identify **blind spots** in your security monitoring.

#### 3. SLA Compliance

**SLA = Service Level Agreement**

An SLA defines **how quickly the SOC is expected to handle an alert/incident within in the promise timeframes**.

**Example:**

```
Company rule: Critical alerts must be acknowledged within 15 minutes.  
100 critical alerts → 95 acknowledged within 15 minutes.  
SLA Compliance = 95%
```

