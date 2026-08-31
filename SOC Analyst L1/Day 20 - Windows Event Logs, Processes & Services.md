# Windows Event Logs

Windows Event Logs are centralized log files that record system, security, application, and user activities on a Windows computer. They help administrators and SOC analysts monitor system health, troubleshoot issues, and detect or investigate security incidents.

**Every Action Generates an Event**

Almost every important activity in Windows creates an event log, such as:

- User login → Event generated
- User logout → Event generated
- Process starts → Event generated
- Service starts/stops → Event generated
- File access → Event generated
- Policy changes → Event generated
- Software installation → Event generated
- System startup/shutdown → Event generated

##### Where Are Event Logs Stored?

**Location:**

```
C:\Windows\System32\winevt\Logs\
```

**File Format:**

```
.evtx
```

### Why Are Event Logs Important for SOC?

Event logs help answer these investigation questions:

- **Who** performed the action?
- **What** happened?
- **When** did it happen?
- **Where** did it happen?
- **How** did it happen?

Without event logs, investigating security incidents becomes extremely difficult.

## Windows Logging Architecture

**Anatomy of a Windows Event Log**

|**Field**|**Description**|
|---|---|
|**Log Name**|The name of the event log.|
|**Source**|The software that logged the event.|
|**XML Data**|All the event information is also included in XML format.|
|**Event ID**|A unique identifier for the event.|
|**Task Category**|A value or name that explains the purpose or use of the event.|
|**Computer**|The name of the computer where the event occurred.|
|**Level**|The severity of the event.|
|**Logged**|The date and time when the event was logged.|
|**Keywords**|More detailed classification of events.|
|**OpCode**|Identifies the specific operation that the event reports.|
|**User**|The user account that was logged on when the event occurred.|

```
Log Name      : Security
Source        : Microsoft-Windows-Security-Auditing
Event ID      : 4624
Task Category : Logon
Computer      : WIN11-PC
Level         : Information
Logged        : 2026-08-02 10:30:15
Keywords      : Audit Success
Opcode        : Info
User          : Administrator
```

---

## What are Security Logs?

**Security Logs** are a type of **Windows Event Log** that record **security-related events**, such as user logins, logouts, failed login attempts, account changes, privilege use, and other security activities.

**Security logs tracks:**
- Authentication (Verifies who the user is)
- Authorization (Determines what the user can access)
- Privileges
- Account changes

These are your primary investigation logs

#### Common Security Event IDs

1. **Logon & Authentication Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4624**|Successful Logon|User successfully logged in.|
|**4625**|Failed Logon|Failed login attempt.|
|**4634**|Logoff|User logged off.|
|**4647**|User Initiated Logoff|User explicitly logged off.|
|**4648**|Logon Using Explicit Credentials|User logged in using different credentials.|
|**4672**|Special Privileges Assigned|Administrative or special privileges assigned after logon.|

2. **Account Management Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4720**|User Account Created|New user account created.|
|**4722**|Account Enabled|User account enabled.|
|**4723**|Password Change Attempt|User attempted to change password.|
|**4724**|Password Reset (by Admin)|Administrator reset a user's password.|
|**4725**|Account Disabled|User account disabled.|
|**4726**|Account Deleted|User account deleted.|

3. **Group & Privilege Management**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4728**|Member Added to Global Group|User added to a global group.|
|**4729**|Member Removed from Global Group|User removed from a global group.|
|**4732**|Member Added to Local Group|User added to a local group.|
|**4733**|Member Removed from Local Group|User removed from a local group.|
|**4756**|Member Added to Universal Group|User added to a universal group.|
|**4757**|Member Removed from Universal Group|User removed from a universal group.|

4. **Process Creation & Execution**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4688**|Process Created|New process started.|
|**4689**|Process Terminated|Process ended.|

5. **Privilege Use Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4673**|Sensitive Privilege Used|Sensitive privilege exercised.|
|**4674**|Operation on Privileged Object|Operation performed on a protected object.|

6. **Authentication (Kerberos / NTLM)**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4768**|Kerberos TGT Request|Initial Kerberos Ticket Granting Ticket requested.|
|**4769**|Kerberos Service Ticket|Service ticket requested.|
|**4771**|Kerberos Pre-auth Failed|Kerberos pre-authentication failed.|
|**4776**|NTLM Authentication|NTLM authentication attempt.|

7. **Object Access Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4656**|Handle Requested|Request for access to an object.|
|**4663**|Object Access Attempt|Object access attempted.|
|**4658**|Handle Closed|Object handle closed.|

8. **Policy & Audit Changes**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4719**|Audit Policy Changed|Audit policy modified.|
|**4739**|Domain Policy Changed|Domain policy modified.|

9. **Log Tampering (Critical)**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**1102**|Security Log Cleared|Windows Security log was cleared. 🚨|

10. **System & Security State Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4608**|Windows Started|Windows system startup.|
|**4609**|Windows Shutdown|Windows system shutdown.|
|**4616**|System Time Changed|System clock modified.|

**Where are Security Logs Stored?**

```
Event Viewer
   │
Windows Logs
   │
Security
```

Physical file location:

```
C:\Windows\System32\winevt\Logs\Security.evtx
```

## What are System Logs?

**System Logs** are a type of **Windows Event Log** that record events related to the**Windows operating system, hardware, device drivers, and system services**.

System Logs are records of everything important happening in the Windows operating system, such as startup, shutdown, driver loading, and service events.

**System logs tracks:**
- OS behavior
- Drivers
- Hardware
- Boot events

#### Common System Event IDs

1. **System Startup & Shutdown Events**

| **Event ID** | **Event**                 | **Description**                             |
| -----------: | ------------------------- | ------------------------------------------- |
|     **6005** | Event Log Service Started | System boot/startup.                        |
|     **6006** | Event Log Service Stopped | Normal shutdown.                            |
|     **6008** | Unexpected Shutdown       | System crashed or lost power unexpectedly.  |
|     **6013** | System Uptime             | Shows how long the system has been running. |

2. **Power & Reboot Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**41**|Kernel-Power|System rebooted without a clean shutdown (power failure, crash, BSOD).|
|**1074**|Planned Shutdown/Restart|System shutdown or restart initiated by a user or process.|
|**109**|Kernel Power Critical Error|Critical power-related error.|

3. **Driver & Hardware Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**219**|Driver Failed to Load|A driver failed to load during system start.|
|**225**|Device Not Migrated|Device did not migrate properly.|
|**11**|Disk Controller Error|Disk controller detected an error.|
|**15**|Device Not Ready|The device is not ready for use.|
|**7**|Bad Block Detected|A bad block was detected on the disk.|

4. **Disk & Storage Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**51**|Disk Warning|An I/O operation was retried or failed on the disk.|
|**55**|NTFS Corruption|The file system structure is corrupted.|
|**98**|NTFS Volume Corruption|Corruption was detected on the volume.|

5. **Service Control Manager Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**7000**|Service Failed to Start|The service failed to start.|
|**7001**|Service Dependency Failed|Required dependent service failed to start.|
|**7009**|Service Timeout|The service did not start in the expected time.|
|**7011**|Service Timeout (No Response)|Service did not respond before timeout.|
|**7034**|Service Crashed Unexpectedly|A running service crashed.|
|**7036**|Service State Changed|Service state changed (Running/Stopped/Paused).|

6. **Network & Connectivity Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**4201**|Network Adapter Connected|A network adapter is connected to the system.|
|**4202**|Network Adapter Disconnected|A network adapter is disconnected from the system.|
|**1014**|DNS Client Events|DNS name resolution has failed.|

7. **Time & System Integrity Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**1**|Time Synchronized|The system time was synchronized.|
|**36**|Time Service Error|Time service encountered an error.|

8. **Crash & Error Reporting Events**

|**Event ID**|**Event**|**Description**|
|--:|---|---|
|**1001**|BugCheck (BSOD)|A Blue Screen of Death occurred.|
|**1000**|Application Error|An application crashed or stopped working.|

9. **Critical System Health Indicators**

|**Event ID**|**Reason**|
|--:|---|
|**41**|Unexpected reboot|
|**6008**|Unexpected shutdown|
|**7, 11, 51, 55, 98**|Disk/File system errors|
|**7034**|Service crashed|
|**1001**|Blue Screen of Death (BSOD)|

**System Logs Cheat Sheet**

|**Issue**|**Key Event IDs**|
|---|---|
|System Crash / Reboot|**41, 6008, 1001**|
|Disk Failure|**7, 51, 55, 98**|
|Service Failure|**7000, 7034**|
|Driver Issue|**219, 225**|
|Network Issue|**1014, 4201, 4202**|

**Use System Logs with Security Logs together for complete visibility of issues and attacks.**

## What is Application Logs?

**Application Logs** are a type of **Windows Event Log** that record events generated by applications and software running on a Windows system.

**Application Logs Record:**
- Application start and stop
- Application crashes
- Application errors
- Warnings
- Software updates
- Database events
- Service-specific events

#### Common Application Event IDs

1. **Application Start & General Events**

|**Event ID**|**Event**|**Description**|
|---|---|---|
|**1000**|Application Error|An application crashed or stopped working unexpectedly.|
|**1001**|Application Hang|The application is not responding.|
|**1002**|Application Unresponsive|The application is unresponsive for a period of time.|
|**1003**|Application Restart|The application was restarted.|
|**1004**|Application Start|The application started successfully.|
|**1005**|Application Stop|The application stopped successfully.|

2. **Application Crash & Failure Events**

| **Event ID** | **Event**                | **Description**                      |
| ------------ | ------------------------ | ------------------------------------ |
| **1006**     | Application Crash        | The application crashed.             |
| **1007**     | Application Fault        | A fault occurred in the application. |
| **1026**     | .NET Runtime Error       | .NET Framework application error.    |
| **1027**     | .NET Runtime Warning     | .NET Framework application warning.  |
| **1028**     | .NET Runtime Information | .NET Framework informational event.  |
| **1029**     | .NET Runtime Debug       | .NET Framework debugging event.      |

3. **Application Install & Update Events**

|**Event ID**|**Event**|**Description**|
|---|---|---|
|**1030**|Application Install|The application was installed.|
|**1031**|Application Uninstall|The application was uninstalled.|
|**1032**|Application Update|The application was updated.|
|**1033**|Configuration Change|Application configuration was changed.|
|**1034**|Configuration Error|Error in application configuration.|

4. **Security & Permission Events**

|**Event ID**|**Event**|**Description**|
|---|---|---|
|**1040**|Application Access Denied|Access to the application was denied.|
|**1041**|Invalid Credentials|Invalid credentials used by the application.|
|**1042**|Login Failure|Application login failed.|
|**1043**|Permission Change|Permissions for the application were changed.|
|**1044**|Security Error|A security-related error occurred.|

5. **Performance & Resource Events**

|**Event ID**|**Event**|**Description**|
|---|---|---|
|**1050**|Performance Warning|Application performance degraded.|
|**1051**|Performance Error|Application performance critical error.|
|**1052**|Resource Warning|Insufficient resources available.|
|**1053**|Resource Error|Critical resource unavailable.|
|**1054**|Timeout|The application operation timed out.|

6. **Application & System Integration Events**

| **Event ID** | **Event**                     | **Description**                                   |
| ------------ | ----------------------------- | ------------------------------------------------- |
| **1060**     | Service Communication Failure | Application failed to communicate with a service. |
| **1061**     | External System Error         | Error communicating with an external system.      |
| **1062**     | Message Queue Error           | Application message queue error.                  |
| **1063**     | Email Send Failure            | Application failed to send email.                 |
| **1064**     | API Call Failure              | Application API call failed.                      |

7. **Audit & Logging Events**

|**Event ID**|**Event**|**Description**|
|---|---|---|
|**1070**|Audit Success|Application audit succeeded.|
|**1071**|Audit Failure|Application audit failed.|
|**1072**|Log Write Success|Log entry written successfully.|
|**1073**|Log Write Failure|Failed to write log entry.|

**Important Application Event IDs at a Glance**

|**Event ID**|**Description**|
|---|---|
|**1000**|Application Error|
|**1001**|Application Hang|
|**1006**|Application Crash|
|**1026**|.NET Runtime Error|
|**1030**|Application Install|
|**1031**|Application Uninstall|
|**1032**|Application Update|
|**1033**|Configuration Change|
|**1040**|Application Access Denied|
|**1051**|Performance Error|
|**1060**|Service Communication Failure|
|**1073**|Log Write Failure|

**Monitor Application Logs regularly to detect crashes, performance issues, security problems and integration failures early.**

--- 

# Windows Processes

A **Windows Process** is a **running instance of a program** that uses system resources like CPU, memory, files, and threads to perform tasks.

A Windows process is a program (in disk) that is executed on your computer and becomes a process (in memory).

**What Does a Process Contain?**

- **Process ID (PID)** – Unique identifier.
- **Threads** – Perform the actual work.
- **Memory** – Stores program data.
- **Handles** – Access files, registry, and other resources.
- **Security Token** – Defines the process's permissions.

```
User Opens Chrome
        │
        ▼
Windows Creates Process
        │
        ▼
Assigns PID
        │
        ▼
Allocates Memory & Threads
        │
        ▼
Program Runs
        │
        ▼
Process Ends When Closed
```

## Windows Process Architecture

```
                         System
                            │
                            ▼
                    smss.exe (Master)
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
     smss.exe (Session 0)        smss.exe (Session 1)
              │                           │
       ┌──────┴──────┐             ┌──────┴──────┐
       ▼             ▼             ▼             ▼
   csrss.exe    wininit.exe    winlogon.exe   csrss.exe
                    │              │
        ┌───────────┼──────────┐   ┴──────────┐
        ▼           ▼          ▼              ▼
   services.exe  lsass.exe  lsaiso.exe   userinit.exe
        │                                    │
        ▼                                    ▼
   svchost.exe                           explorer.exe
                                  
                                  
                             
```

|**Process**|**Explanation**|
|---|---|
|**System**|The Windows kernel process that starts during boot and manages low-level system operations.|
|**smss.exe (Master)**|**Session Manager Subsystem**. First user-mode process started by the kernel; creates and manages Windows sessions.|
|**smss.exe (Session 0)**|Creates the system session used for Windows services and background processes.|
|**smss.exe (Session 1)**|Creates the user session used for interactive user login and desktop environment.|
|**csrss.exe**|**Client Server Runtime Process**. Handles Windows console operations and user-mode graphical functions.|
|**wininit.exe**|Windows Initialization Process. Starts essential system processes like services.exe, lsass.exe, and lsaiso.exe.|
|**winlogon.exe**|Handles user login/logout, authentication interface, and starts the user environment after successful login.|
|**services.exe**|**Service Control Manager (SCM)**. Manages Windows services and starts/stops background services.|
|**svchost.exe**|**Service Host Process**. Hosts and runs multiple Windows services that run as DLL-based services.|
|**lsass.exe**|**Local Security Authority Subsystem Service**. Handles authentication, security policies, and stores authentication-related information.|
|**lsaiso.exe**|**LSA Isolated Process**. Protects sensitive authentication data by isolating LSASS operations (used with Credential Guard).|
|**userinit.exe**|Initializes the user's environment after login and starts the Windows user shell.|
|**explorer.exe**|Windows Shell process that provides the desktop, taskbar, Start menu, and File Explorer interface.|

## Process Life Cycle (Windows Process States)

#### 1. New State

- A new process is created by the operating system to execute a program.

**Example:**

- You open Chrome → Windows creates a new Chrome process.
#### 2. Ready State

- The process is ready to run but waiting for CPU allocation.

**Example:**

- Chrome is loaded into memory but waiting for CPU time.
#### 3. Running State

- The process is currently executing instructions using the CPU.

**Example:**

- You are browsing in Chrome, so the Chrome process is running.

#### 4. Waiting / Blocked State

- The process cannot continue running because it is waiting for a resource or event.

**Reasons:**

- Waiting for user input.
- Waiting for network response.
- Waiting for a file operation.
- Waiting for a signal from another process.

**Example:**

- A browser waits while a webpage loads from the internet.
#### 5. Terminated State

- The process has completed execution or has been stopped by the operating system.

**Example:**

- You close Chrome → Chrome process terminates.

```
New
 │
 ▼
Ready
 │
 ▼
Running
 │
 ├──────────────► Terminated
 │
 ▼
Waiting
 │
 ▼
Ready
```

- **New** → Process is created.
- **Ready** → Waiting for CPU.
- **Running** → Executing.
- **Waiting** → Waiting for resource/event.
- **Terminated** → Process finished.

## Critical Windows System Processes

| **Process Name**             | **Process File** | **Description**                                                                                | **Importance** | **Impact If Terminated**                      |
| ---------------------------- | ---------------- | ---------------------------------------------------------------------------------------------- | -------------- | --------------------------------------------- |
| **System**                   | ntoskrnl.exe     | Windows NT kernel process. Manages hardware, memory, processes, and system resources.          | Critical       | System will crash immediately (BSOD).         |
| **smss.exe**                 | smss.exe         | Session Manager Subsystem. Starts user sessions and critical system processes.                 | Critical       | System may fail to start or shut down.        |
| **csrss.exe**                | csrss.exe        | Client/Server Runtime Subsystem. Handles Win32 subsystem and console windows.                  | Critical       | Applications and system UI will stop working. |
| **wininit.exe**              | wininit.exe      | Windows initialization process. Starts services and userinit.exe.                              | Critical       | System may become unusable.                   |
| **services.exe**             | services.exe     | Service Control Manager. Manages Windows services.                                             | Critical       | Many services will stop; system instability.  |
| **lsass.exe**                | lsass.exe        | Local Security Authority Subsystem. Handles authentication, security policies, and user logon. | Critical       | Logon will fail; security functions stop.     |
| **svchost.exe**              | svchost.exe      | Generic Host Process for Windows services. Runs multiple Windows services.                     | Critical       | Dependent services will stop.                 |
| **explorer.exe**             | explorer.exe     | Windows Explorer. Manages desktop, taskbar, Start menu, and File Explorer.                     | High           | Desktop, taskbar, and UI will disappear.      |
| **spoolsv.exe**              | spoolsv.exe      | Print Spooler. Manages print jobs and printer communication.                                   | High           | Printing will not work.                       |
| **taskhostw.exe**            | taskhostw.exe    | Hosts tasks scheduled by users or Windows Task Scheduler.                                      | Medium         | Scheduled tasks may not run.                  |
| **dwm.exe**                  | dwm.exe          | Desktop Window Manager. Provides visual effects and window management.                         | Medium         | Affects UI performance and visuals.           |
| **svchost.exe (DNS Client)** | svchost.exe      | Hosts DNS Client service. Resolves domain names.                                               | Medium         | Internet name resolution may fail.            |
| **svchost.exe (Power)**      | svchost.exe      | Hosts Power service. Manages power settings.                                                   | Medium         | Power management issues.                      |
| **wuauclt.exe**              | wuauclt.exe      | Windows Update Client. Checks for and installs updates.                                        | Low            | Windows updates may not work.                 |
| **MsMpEng.exe**              | MsMpEng.exe      | Microsoft Defender Antivirus engine process.                                                   | Low            | System protection may be disabled.            |

## Process Based Attacks

**Process-Based Attacks** are cyber attacks where an attacker **abuses, injects into, hijacks, or creates processes** to execute malicious code, evade detection, steal data, or gain persistence.

|**Attack**|**Description**|
|---|---|
|**Process Injection**|Injects malicious code into a legitimate process.|
|**Process Hollowing**|Starts a legitimate process, removes its code, and replaces it with malware.|
|**DLL Injection**|Forces a process to load a malicious DLL.|
|**Process Masquerading**|Uses a fake process name to look like a legitimate Windows process.|
|**Process Doppelgänging**|Executes malware by abusing NTFS transactions, making detection difficult.|
|**Process Ghosting**|Runs malware from a deleted executable to evade security tools.|
|**Parent PID (PPID) Spoofing**|Makes a malicious process appear to have a trusted parent process.|
|**Privilege Escalation via Process Token**|Steals or duplicates another process's access token to gain higher privileges.|

## SOC Detection

Monitor for:

- Unusual parent-child process relationships.
- Unknown or unsigned executables.
- Suspicious process injection.
- `powershell.exe`, `cmd.exe`, `rundll32.exe`, `regsvr32.exe`, `mshta.exe` started unexpectedly.
- Processes running from unusual locations (e.g., `AppData`, `Temp`).
- High CPU or memory usage by unknown processes.

---

# Windows Services

**Windows Services** are background programs that run automatically in Windows without user interaction and starts automatically when system boot.

**Examples of Windows Services**

- Windows Services
- Antivirus
- Print spooler (Manages printing tasks)
- DHCP Client
- Remote Desktop Services

## How Windows Services Work

- Windows boots and starts **`services.exe` (Service Control Manager - SCM)**.
- SCM reads the list of installed services from the **Windows Registry** (`HKLM\SYSTEM\CurrentControlSet\Services`).
- SCM checks each service's **startup type** (Automatic, Manual, Disabled).
- SCM starts the required services based on their startup type.
- Services run either as their own process (e.g., `spoolsv.exe`) or inside **`svchost.exe`**.
- Running services perform background tasks like networking, updates, printing, and security.
- SCM continuously monitors services and can stop, start, pause, or restart them if needed.
- Services continue running in the background until Windows shuts down or the service is stopped.

```
Windows Boot
      │
      ▼
services.exe (SCM)
      │
      ▼
Reads Registry
      │
      ▼
Checks Startup Type
      │
      ▼
Starts Required Services
      │
      ▼
Services Run (svchost.exe / own process)
      │
      ▼
SCM Monitors Services
```


### SCM (Service Control Manager)

The **Service Control Manager (SCM)** is a core Windows component that **manages all Windows services**. It is responsible for starting, stopping, monitoring, and controlling services during system startup and while Windows is running.

- Starts Windows services.
- Stops Windows services.
- Restarts failed services (if configured).
- Monitors service status.
- Reads service configuration from the Windows Registry.
- Manages service dependencies.
- Controls service startup types.

**Where are Windows Services Stored?**

Windows stores the configuration of every service in the **Windows Registry**.

```
HKLM\SYSTEM\CurrentControlSet\Services
```

**Each Service Contains**

|**Field**|**Description**|
|---|---|
|**Service Name**|The unique name used to identify the service.|
|**Image Path**|The path of the executable (.exe) or DLL that the service runs.|
|**Start Type**|Defines when the service starts (Automatic, Manual, Disabled, etc.).|
|**Permissions**|Specifies which users or processes can start, stop, or modify the service.|

#### Types of Windows Services

##### 1. Kernel Services

- Services that run in **Kernel Mode** and interact directly with hardware.

**Examples:**

- Device Drivers
- Storage Drivers
- Network Drivers

**Purpose:**

- Manage hardware devices and low-level system operations.

##### 2. File System Services

- Services that manage file systems and disk operations.

**Examples:**

- NTFS File System
- Disk Drivers

**Purpose:**

- Read, write, and manage files and storage devices.

##### 3. User-Mode Services

- Services that run in **User Mode** and perform background tasks without directly accessing hardware.

**Examples:**

- Windows Update
- Print Spooler
- Windows Defender
- DNS Client
- DHCP Client

**Purpose:**

- Provide networking, security, printing, updates, and other background functions.

### Service Startup Types

|**Startup Type**|**Meaning**|
|---|---|
|**Automatic**|Starts automatically when Windows boots.|
|**Manual**|Starts only when required by Windows or a user/application.|
|**Disabled**|Cannot start unless it is enabled first.|

## What is svchost.exe?

svchost.exe is a container process that runs multiple Windows services in the background.

- It hosts multiple services

## Common Attack Techniques Using Windows Services

|**Attack Technique**|**Definition**|**Example**|**SOC Detection**|
|---|---|---|---|
|**Malicious Service Installation**|Attacker creates a new Windows service to run malware automatically.|`UpdateService → C:\Users\Temp\malware.exe`|Monitor **Event ID 7045**, unknown service names, and services running from `AppData` or `Temp`.|
|**Service Hijacking**|Attacker changes a legitimate service's executable path to run malware.|`legit.exe → malware.exe`|Check **ImagePath** changes, Registry modifications, and verify file signatures.|
|**Privilege Escalation via Services**|Attacker exploits a vulnerable or misconfigured service to gain **SYSTEM** privileges.|Writable service running as **SYSTEM**.|Monitor service permission changes and suspicious privilege escalation activity.|
|**Persistence**|Malware installs a service that starts automatically after every reboot.|Fake service with **Automatic** startup.|Detect newly created auto-start services and revie|
