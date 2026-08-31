# Endpoint Detection & Response (EDR)

**EDR is a security solution that continuously monitors computers and other endpoints to detect, investigate, and respond to suspicious or malicious and ransomware activity.**

- It is also referred to as endpoint detection and threat response (EDTR)

|Function|Simple Meaning|
|---|---|
|**Endpoint**|A device such as a laptop, PC, or server|
|**Detection**|Finds suspicious or malicious activity|
|**Investigation**|Helps analysts understand what happened|
|**Response**|Takes action against the threat|
|**Monitoring**|Continuously watches endpoint activity|

### Below are some of the EDR solutions in the market:

- CrowdStrike Falcon
- SentinelOne ActiveEDR
- Microsoft Defender for Endpoint
- OpneEDR
- Symantec EDR

##### What can EDR monitor?

- Processes and applications
- Files and file modifications
- PowerShell/command-line activity
- Network connections
- User activity
- Registry/system changes
- Malware behavior

### How EDR Works

**EDR (Endpoint Detection & Response)** works by installing an **agent on each endpoint** and continuously monitoring its activity. The collected data is analyzed for suspicious behavior, then alerts and response actions are generated.

|Step|What Happens|Simple Meaning|
|---|---|---|
|**1. EDR Agent**|An agent is installed on the endpoint|Security sensor on the laptop/server|
|**2. Data Collection**|Agent collects process, file, network, registry, and other endpoint activity|EDR watches what is happening|
|**3. Data Analysis**|Activity is analyzed using rules, signatures, behavioral detection, and sometimes ML|Is this normal or suspicious?|
|**4. Threat Detection**|Suspicious behavior is identified|EDR detects a possible attack|
|**5. Alert Generation**|EDR creates an alert with relevant evidence|SOC gets notified|
|**6. Investigation**|Analyst examines the activity and related events|What happened? How did it happen?|
|**7. Response**|EDR can take actions such as isolating the endpoint or terminating a malicious process|Stop/contain the attack|
|**8. Recovery**|Security team removes the threat and restores the endpoint|Return the system to a safe state|

##### Example

Imagine a user downloads **malware.exe**:

```
User downloads malware.exe
        ↓
EDR Agent observes the file
        ↓
malware.exe starts a suspicious process
        ↓
Process tries to modify system files
        ↓
EDR detects suspicious behavior
        ↓
🚨 Alert sent to SOC
        ↓
Analyst investigates
        ↓
EDR isolates the endpoint
        ↓
Threat is removed
```


### EDR Example

- **Visibility** → EDR records what is happening on the endpoint.
    - Example: User opens a PDF.
    - The PDF launches a hidden/background script.
- **Detection** → EDR analyzes the activity and looks for **suspicious behavior**.
    - Example: The script tries to access or steal credentials.
    - EDR detects the suspicious activity and generates an **alert**.
- **Response** → EDR takes action against the threat.
    - **Isolates the laptop** from the network.
    - **Stops/terminates the malicious process or script**.
    - Helps prevent the attacker from continuing the attack.

# How EDR works (The Operational Flow)

EDR (**Endpoint Detection and Response**) works in a continuous **4-stage process**:

### 1. Data Collection

- An **EDR agent** runs on the endpoint (laptop, desktop, server, VM).
- It continuously collects **telemetry** such as:
    - Process executions
    - Network connections
    - File creation/modification
    - Registry changes
    - User/login activity

**Example:** A user opens a PDF → `pdf.exe` starts → `cmd.exe` → `powershell.exe`.

### 2. Detection & Analysis

- The collected data is sent to the **EDR management/cloud console**.
- The EDR analyzes the activity using:
    - Behavioral rules
    - Threat intelligence
    - Machine learning/AI
    - Known indicators/signatures
- It looks for **suspicious behavior**, not just known malware files.

**Example:**  
PDF → PowerShell → suspicious command → credential access  
➡️ EDR identifies this as suspicious and generates an **alert**.

### 3. Investigation & Response

- The SOC analyst investigates the alert.
- EDR provides a **timeline** showing what happened before and after the detection.
- The analyst can determine:
    - How the attack started
    - Which processes ran
    - Which files were created
    - Which IPs the machine contacted
    - Whether credentials were targeted

### 4. Containment & Remediation

EDR can take immediate action, either automatically or manually:

- **Isolate the endpoint** from the network
- **Terminate malicious processes**
- Quarantine/delete malicious files
- Block malicious hashes or indicators
- Remove persistence mechanisms
- Restore/clean the endpoint

```
Endpoint
↓
EDR Agent collects telemetry
↓
EDR analyzes behavior
↓
Suspicious activity detected
↓
Alert generated
↓
SOC investigates
↓
Endpoint isolated / process terminated
↓
Threat removed & system recovered
```

## EDR vs Traditional Antivirus

|Feature|Traditional Antivirus (AV)|EDR|
|---|---|---|
|**Detection**|Mainly looks for **known malicious files/signatures**|Looks for **suspicious behavior and activity**|
|**Data Collection**|Usually records mainly **detections/blocked events**|Continuously collects **endpoint activity/telemetry**|
|**Visibility**|Limited visibility into attack activity|Detailed visibility into **processes, scripts, network connections, memory activity, etc.**|
|**Response**|Mainly **quarantines/deletes files**|Can **isolate the endpoint, terminate processes, quarantine files, and investigate remotely**|

# EDR Process Tree

A **process tree** shows the relationship between processes — basically **which process started/spawned which process**.

```
[1] outlook.exe
      ↓
[2] chrome.exe
      ↓
[3] invoice_9932.pdf.exe
      ↓
[4] cmd.exe
      ↓
[5] powershell.exe
```

- **`outlook.exe`**
    - User receives/opens an email.
- **`chrome.exe`**
    - User clicks a link in the email.
    - The browser opens.
- **`invoice_9932.pdf.exe`**
    - A malicious executable is downloaded.
    - It is named to look like a PDF.
    - ⚠️ Suspicious because the real extension is `.exe`.
- **`cmd.exe`**
    - The malicious program launches the Windows command shell.
- **`powershell.exe`**
    - `cmd.exe` launches PowerShell.
    - PowerShell executes the attacker's script/commands.
    - EDR detects this suspicious execution and generates an alert.

##### This helps the analyst determine:

- **Where the attack started**
- **Which process caused the suspicious activity**
- **What the attacker executed**
- **What happened before and after the alert**
- **Whether other machines may be affected**

