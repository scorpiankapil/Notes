# Lateral Movement

**Lateral Movement** is the technique where an attacker **moves from one compromised system to other systems within the same network** to gain access to more computers, servers, or sensitive data.

Instead of leaving the network, the attacker moves sideways across machines.

- Find valuable data
- Reach domain controllers
- Access admin accounts
- Deploy ransomware across the network

#### Why Do Attackers Perform Lateral Movement?

Because the first compromised system rarely has valuable data.

- Reach high-value systems (servers, domain controllers).
- Steal sensitive data.
- Gain higher privileges.
- Expand control within the network.
- Deploy ransomware across multiple systems.

## Common Lateral Movement Techniques

## Pass-the-Hash (PtH)

**Pass-the-Hash (PtH)** is a cyberattack technique where an attacker uses a stolen password hash to authenticate to another system without knowing or cracking the actual password.

In a Pass-the-Hash attack:

- The attacker **doesn't know the password**.
- The attacker **already has the password hash**.
- They **pass (use) the hash directly** to authenticate.

Hence the name **Pass-the-Hash**.

##### Common Tools

|Tool|Purpose|
|---|---|
|**Mimikatz**|Extracts password hashes and credentials from Windows memory.|
|**CrackMapExec**|Uses stolen hashes to authenticate to remote systems and perform lateral movement.|

##### SOC Detection Indicators

- Unusual NTLM authentication events.
- Logins without interactive password entry.
- One account logging into multiple systems quickly.
- Lateral movement between hosts.
- Suspicious credential usage.
- Execution of credential-dumping tools (e.g., Mimikatz).
- Windows Event ID **4776** (NTLM authentication) from unusual hosts.

## Pass-the-Ticket (Kerberos Attack)

**Pass-the-Ticket (PtT)** is a cyberattack technique where an attacker **steals a Kerberos authentication ticket** and uses it to access other systems **without knowing the user's password**.

Unlike Pass-the-Hash, which uses an **NTLM hash**, Pass-the-Ticket uses a **Kerberos ticket**.

##### Common Tools

|Tool|Purpose|
|---|---|
|**Mimikatz**|Extracts and injects Kerberos tickets from memory.|
|**Rubeus**|Requests, extracts, and abuses Kerberos tickets.|

##### How Pass-the-Ticket (PtT) Works

1. User logs in to the Windows domain.
2. The Domain Controller (KDC) authenticates the user.
3. A **Kerberos Ticket Granting Ticket (TGT)** is issued.
4. The ticket is stored in the user's memory (LSASS).
5. The attacker compromises the victim's computer.
6. The attacker steals the Kerberos ticket using tools like **Mimikatz** or **Rubeus**.
7. The attacker injects or reuses the stolen ticket.
8. The attacker authenticates to other systems without knowing the user's password.
9. The attacker moves laterally across the network to access additional systems and resources.
##### SOC Detection Indicators

- Unusual Kerberos authentication activity.
- Ticket usage from unexpected devices.
- Multiple systems accessed using the same Kerberos ticket.
- Abnormal Ticket Granting Ticket (TGT) or Service Ticket (TGS) requests.
- Logins without a normal interactive authentication process.
- Suspicious activity from privileged accounts.

## Remote Desktop Protocol (RDP)

**Remote Desktop Protocol (RDP)** is a Microsoft protocol that allows a user to remotely access and control another Windows computer over a network.

It uses **TCP Port 3389** by default.

##### SOC Detection Indicators

- Unusual internal RDP connections.
- RDP logins from unexpected devices or IP addresses.
- Login attempts outside normal working hours.
- Multiple RDP logins using the same account.
- RDP connections to critical servers.
- Multiple failed RDP login attempts (possible brute force).
- RDP enabled on systems where it is normally disabled.

## SMB (Server Message Block) / Windows Admin Shares

**SMB (Server Message Block)** is a network protocol that allows computers to **share files, folders, printers, and other resources** over a network.

- **Port 445**
##### What are Windows Administrative Shares?

Windows automatically creates hidden administrative shares such as:

- **C$** → C: drive
- **ADMIN$** → Windows system directory
- **IPC$** → Inter-Process Communication

These shares are used by **administrators for remote management**.

##### What is `\\target\C$`?

```
\\target\C$
```

- `target` = Remote Windows computer.
- `C$` = Hidden administrative share for the C: drive.

##### Common Tools

|Tool|Purpose|
|---|---|
|**PsExec**|Remotely executes commands or programs on Windows systems using SMB.|
|**Impacket**|A toolkit that includes tools for SMB, NTLM, Kerberos, and remote command execution.|
|**CrackMapExec**|Automates SMB enumeration, authentication, and lateral movement across Windows networks.|

##### SOC Detection Indicators

- Access to administrative shares (`C$`, `ADMIN$`, `IPC$`).
- Unusual SMB connections (Port 445).
- Suspicious file transfers between systems.
- Remote service creation events.
- PsExec execution.
- Remote command execution.
- Multiple SMB connections from one host.

## Windows Management Instrumentation (WMI)

**Windows Management Instrumentation (WMI)** is a Windows management framework that allows administrators to **remotely manage, monitor, and execute commands on Windows computers.**

- Execute commands remotely.
- Run malware on another computer.
- Create or terminate processes.
- Move laterally without using RDP.

```
wmic /node:kapil process call create "malware.exe"
```

- `wmic` → Windows Management Instrumentation Command-line.
- `/node:target` → Connect to the remote computer named **kapil**.
- `process` → Manage Windows processes.
- `call create` → Create (start) a new process.
- `"malware.exe"` → Program to run on the remote computer.

##### SOC Detection Indicators

- Unusual WMI process creation.
- Remote command execution events.
- WMI activity from unexpected hosts.
- WMI execution outside business hours.
- One system remotely executing commands on multiple computers.
- Suspicious child processes launched by **wmiprvse.exe**.

---

# Privilege Escalation

**Privilege Escalation** is the process by which an attacker gains **higher-level permissions or privileges** on a system after initially gaining access.

For example, an attacker who compromises a **normal user account** tries to become an **administrator or root user**.

- Gain administrator or root access.
- Disable security software.
- Access sensitive files.
- Install malware.
- Create new administrator accounts.
- Move laterally to other systems.

## Types of Privilege Escalation

## 1. Vertical Privilege Escalation

**Vertical Privilege Escalation** is in which a user or attacker gains **higher privileges or permissions** than they are authorized to have. The attacker moves from a **lower privilege level to a higher privilege level**, such as from a normal user to an administrator or root user.

- Moves **up** to a higher privilege level.
- Involves gaining administrative or root access.
- Can lead to complete system compromise.

```
Normal User -> Local Admin -> Domain Admin
```

## 2. Horizontal Privilege Escalation

**Horizontal Privilege Escalation** is in which a user or attacker accesses or modifies **another user's resources** while remaining at the **same privilege level**. The attacker does **not** gain additional permissions but abuses weak authorization checks to access data belonging to other users.

The attacker **does not gain higher privileges** but accesses **another user's account with the same privilege level**.

- Remains at the **same** privilege level.
- Targets another user's data or account.
- Commonly caused by **Broken Access Control** or **IDOR (Insecure Direct Object Reference)**.

```
User -> Another User
```

# Common Privilege Escalation Techniques (Single Points)

### 1. Exploiting Software Vulnerabilities

- Exploiting unpatched software or OS vulnerabilities to gain administrator or root privileges.
- Example: Outdated Windows kernel, vulnerable drivers.

### 2. Credential Dumping

- Extracting passwords, hashes, or credentials from system memory to gain privileged access.
- Example: Mimikatz, LSASS memory dumping.

### 3. Misconfigured Permissions

- Abusing incorrect file, folder, or service permissions to obtain higher privileges.
- Example: Writable service executable running as SYSTEM.

### 4. Token Impersonation

- Stealing and using a privileged Windows access token to impersonate an administrator or SYSTEM account.

### 5. Scheduled Task Abuse

- Modifying or creating scheduled tasks that run with administrator or SYSTEM privileges to execute malicious code.

# SOC Indicators of Privilege Escalation

##### Watch For

- Sudden administrator rights assignment.
- Creation of new administrator accounts.
- Unexpected service creation events.
- Suspicious access to the LSASS process.
- Privilege escalation exploit activity.
- Unauthorized changes to user or group permissions.
- Execution of known privilege escalation tools.

`LSASS Process - LSASS (Local Security Authority Subsystem Service) is a Windows system process responsible for handling user authentication, password verification, security policies, and access tokens.`

`Process name - lsass.exe`

#### Important Windows Event IDs

|Event ID|Meaning|
|---|---|
|**4672**|Special privileges assigned to a user account (e.g., Administrator/SYSTEM login).|
|**4688**|A new process was created (useful for detecting exploit or privilege escalation tools).|
|**4720**|A new user account was created.|
|**4732**|A user was added to a privileged/local administrator group.|

---
# Lateral Movement vs Privilege Escalation

|**Lateral Movement**|**Privilege Escalation**|
|---|---|
|Moving from one compromised system to another within the network.|Gaining higher permissions or privileges on a system.|
|Goal is to access more systems and resources.|Goal is to become an administrator or root user.|
|Uses stolen credentials, hashes, or Kerberos tickets.|Exploits vulnerabilities or misconfigurations to gain higher privileges.|
|Occurs **after initial access** to expand through the network.|Occurs **after initial access** to gain greater control on the current system.|
|Targets **other computers** in the network.|Targets the **same compromised computer**.|
|Helps attackers reach critical assets (servers, Domain Controller).|Helps attackers disable security controls, access sensitive files, and install malware.|
|Common techniques: Pass-the-Hash, Pass-the-Ticket, RDP, SMB, WMI.|Common techniques: Exploiting vulnerabilities, Credential Dumping, Token Impersonation, Misconfigured Permissions, Scheduled Task Abuse.|
|**SOC Indicators:** Unusual RDP/SMB/WMI activity, multiple logins across hosts, abnormal Kerberos/NTLM authentication.|**SOC Indicators:** New admin accounts, privilege assignments, LSASS access, service creation, Event IDs 4672, 4688, 4720, 4732.|
