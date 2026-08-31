  n # Windows Architecture

**Windows Architecture** is the internal design and structure of the Windows operating system. It defines **how hardware, the operating system, applications, and users interact** to perform tasks securely and efficiently.

**Windows Architecture defines:** 
- How process run
- How memory handle
- How user authenticate
- How security is enforced

In SOC, this = where attack happen

## Windows Architecture Diagram


```
                USER MODE (Ring 3)
+---------------------------------------------------+
| User Applications                                 |
| Chrome | Edge | Notepad | Word | Games            |
+---------------------------------------------------+
| Windows Subsystems                                |
| Win32 API | .NET Runtime | POSIX (Legacy)         |
+---------------------------------------------------+
| System DLLs                                       |
| kernel32.dll | user32.dll | advapi32.dll          |
+---------------------------------------------------+
                    │
              System Calls (API)
                    │
                    ▼
             KERNEL MODE (Ring 0)
+---------------------------------------------------+
| Executive                                         |
| Object Manager                                    |
| Process Manager                                   |
| Memory Manager                                    |
| I/O Manager                                       |
| Security Reference Monitor                        |
| Cache Manager                                     |
| Plug and Play Manager                             |
| Power Manager                                     |
+---------------------------------------------------+
| Windows Kernel (ntoskrnl.exe)                     |
+---------------------------------------------------+
| Device Drivers                                    |
+---------------------------------------------------+
| HAL (Hardware Abstraction Layer)                  |
+---------------------------------------------------+
| Hardware (CPU, RAM, Disk, Network, USB, GPU)      |
+---------------------------------------------------+
```

- **Ring 0** has the **highest privilege**.
- **Ring 3** has the **lowest privilege**.

```
+-------------------------------+
| Ring 3 - User Applications    |  Lowest Privilege
+-------------------------------+
| Ring 2 - Device Services      |  Rarely Used
+-------------------------------+
| Ring 1 - Device Drivers       |  Rarely Used
+-------------------------------+
| Ring 0 - Kernel               |  Highest Privilege
+-------------------------------+
```


#### Ring 0 (Kernel Mode)

Ring 0 is the **highest privilege level**. It runs the **Windows Kernel**, device drivers, and core operating system components.

- Highest privilege level.
- Direct access to CPU, RAM, and hardware.
- Can execute privileged CPU instructions.
- Can access all memory.
- A crash in Ring 0 can crash the entire operating system (BSOD).

#### Ring 1

Ring 1 is an intermediate privilege level intended for **device drivers or operating system services**.

- Lower privilege than Ring 0.
- Higher privilege than Ring 2 and Ring 3.
- Supported by the CPU.

- `Not used by modern Windows.`
- `Windows runs drivers directly in Ring 0.`

#### Ring 2

Ring 2 is another intermediate privilege level intended for **system services or device drivers**.

- More privileged than Ring 3.
- Less privileged than Ring 1 and Ring 0.

- `Not used by modern Windows.`

#### Ring 3 (User Mode)

Ring 3 is the **lowest privilege level**, where normal user applications execute.

- Limited privileges.
- Cannot directly access hardware.
- Cannot access kernel memory.
- Must request services through system calls.


|Ring|Privilege Level|Purpose|Windows Usage|
|---|---|---|---|
|**Ring 0**|Highest|Kernel, device drivers, hardware access|Used|
|**Ring 1**|High|Device drivers, OS services|Not Used|
|**Ring 2**|Medium|Device drivers, OS services|Not Used|
|**Ring 3**|Lowest|User applications|Used|

### Why Doesn't Windows Use Ring 1 and Ring 2?

- **Simplifies the operating system architecture**, making Windows easier to design and maintain.
- **Improves performance** by reducing the number of privilege-level (ring) switches.
- **Most device drivers require full hardware access**, so they run directly in **Ring 0**.
- **Ensures better compatibility** with hardware and third-party drivers.
- **Reduces system complexity**, making development and troubleshooting easier.
- **Windows NT was designed to use only Ring 0 (Kernel Mode) and Ring 3 (User Mode)**, and this design continues in modern Windows.
- **Ring 1 and Ring 2 are supported by the CPU but remain unused** in modern Windows operating systems.

# Two Mode (Windows Architecture)

| **User Mode**                           | **Kernel Mode**                                |
| --------------------------------------- | ---------------------------------------------- |
| Runs at **Ring 3**                      | Runs at **Ring 0**                             |
| Limited privileges                      | Full privileges                                |
| Runs applications                       | Runs Windows kernel and drivers                |
| No direct hardware access               | Direct hardware access                         |
| Uses system calls to access OS services | Directly manages hardware and system resources |
| Crash affects only the application      | Crash may cause a BSOD                         |

# User Mode

**User Mode** is the part of Windows where **user applications and programs run with limited privileges**. Programs running in User Mode **cannot directly access hardware or kernel memory**. They must request services from the operating system through **system calls**.

- Runs at **Ring 3** (lowest privilege level).
- Runs user applications and services.
- Cannot directly access hardware.
- Cannot directly access kernel memory.
- Uses **system calls** to request services from the kernel.
- If an application crashes, only that application is affected—not the entire operating system.

### SOC Perspective

- Most legitimate applications run in User Mode.
- Malware often starts in User Mode before attempting **privilege escalation** to Kernel Mode.
- Suspicious User Mode processes (e.g., unusual PowerShell or command prompt activity) are common indicators of compromise.
- Monitoring User Mode processes helps detect malware, code injection, and unauthorized execution.

# Kernel Mode

**Kernel Mode** is the privileged mode of the Windows operating system where the **Windows kernel, device drivers, and core system components run with full access to the computer's hardware and memory.**

- Runs at **Ring 0** (highest privilege level).
- Has full access to CPU, RAM, and hardware.
- Can execute privileged CPU instructions.
- Manages memory, processes, files, and devices.
- Runs the Windows kernel and device drivers.
- A crash in Kernel Mode can cause a **Blue Screen of Death (BSOD).**

### SOC Perspective

- Install **rootkits (a type of malware designed to hide itself and other malicious software from the operating system)**.
- Rootkit operate here
- Disable antivirus or EDR.
- Dump credentials from **LSASS**.
- Load malicious drivers.
- Hide malicious processes and files.
- Gain complete control of the system.

---

# Windows Architecture

The **Windows Kernel** is the **core (heart) of the Windows Operating System**. It acts as a bridge between **software (applications)** and **hardware (CPU, RAM, Disk, Keyboard, etc.)** and manages all the critical system resources.

## What Exactly Does the Windows Kernel Do?

- **Manages Processes** – Creates, schedules, and terminates running processes.
- **Manages Memory** – Allocates RAM, manages virtual memory, and protects process memory.
- **Controls Hardware Devices** – Communicates with hardware through device drivers.
- **Manages File System** – Reads/writes files and handles disk I/O operations.
- **Schedules CPU Time** – Decides which process gets CPU time for smooth multitasking.
- **Provides Security** – Enforces permissions, access control, and memory protection.
- **Handles Hardware Interrupts** – Responds to events from devices like the keyboard, mouse, disk, and network.
- **Manages Network Operations** – Processes network traffic and communicates with network drivers.

## Executive Layer in Windows Kernel

The Executive Layer is a component of the Windows Kernel that provides essential operating system services by managing processes, memory, security, files, devices, and other system resources.

#### 1. Object Manager

- Manages system objects (files, processes, threads, events, mutexes).
- Provides object naming and handles.

**Example:** Opening a file creates a file object managed by the Object Manager.

#### 2. Process Manager

- Creates and terminates processes.
- Creates and manages threads.
- Tracks process information.

**Example:** Starting Chrome creates a new process.

#### 3. Virtual Memory Manager

- Allocates and frees memory.
- Manages virtual memory.
- Handles paging and swapping.
- Protects memory between processes.

#### 4. I/O Manager

- Manages input/output requests.
- Communicates with device drivers.
- Routes I/O Request Packets (IRPs).

**Example:** Reading a file from disk.

#### 5. Security Reference Monitor (SRM)

- Enforces security policies.
- Performs access checks.
- Validates user permissions.

**Example:** Checking whether a user can open a protected file.

#### 6. Cache Manager

- Caches frequently accessed file data in RAM.
- Reduces disk access.
- Improves file system performance.

#### 7. Plug and Play (PnP) Manager

- Detects new hardware.
- Loads the correct drivers.
- Configures hardware automatically.

**Example:** Connecting a USB flash drive.

#### 8. Power Manager

- Controls power states.
- Manages sleep, hibernation, and shutdown.
- Optimizes battery usage.

#### 9. Configuration Manager

- Manages the Windows Registry.
- Reads and writes registry settings.
- Loads system configuration during boot.

#### 10. LPC/ALPC Manager (Local Procedure Call)

- Enables communication between processes on the same system.
- Used by Windows services and system components for fast inter-process communication (IPC).

|Component|Function|
|---|---|
|**Object Manager**|Manages system objects and handles|
|**Process Manager**|Creates and manages processes and threads|
|**Virtual Memory Manager**|Manages RAM and virtual memory|
|**I/O Manager**|Handles input/output operations|
|**Security Reference Monitor**|Enforces security and permissions|
|**Cache Manager**|Speeds up file access using cache|
|**Plug and Play Manager**|Detects and configures hardware|
|**Power Manager**|Manages power states|
|**Configuration Manager**|Manages the Windows Registry|
|**LPC/ALPC Manager**|Enables inter-process communication|

### Hardware Abstraction Layer (HAL)

The Hardware Abstraction Layer (HAL) is a software layer that acts as a bridge between the Windows Kernel and the hardware, allowing the operating system to communicate with different hardware devices in a uniform way.

- Hides hardware complexity from the kernel.
- Provides a common interface for different hardware.
- Improves compatibility with different CPUs and motherboards.
- Makes Windows portable across different hardware platforms.
- Simplifies hardware communication.

### Windows Process Architecture

Windows Process Architecture is the internal framework that Windows uses to create, execute, schedule, manage, and terminate processes and threads while handling memory, security, CPU scheduling, and other system resources efficiently.

It is fundamental unit managed by the operating system, identified by a unique **process identifier (PID)**

```
                User Starts a Program
                        │
                        ▼
                 Executable File (.exe)
                        │
                        ▼
               Windows Process Manager
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
   Create Process   Allocate Memory   Create Threads
        │               │                │
        └───────────────┼────────────────┘
                        ▼
                 Process Execution
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
   CPU Scheduling   File I/O      Network I/O
                        │
                        ▼
                Process Terminates
                        │
                        ▼
              Resources are Released
```


##### These are some of the **most important Windows system processes** that every SOC analyst, DFIR analyst, or pentester should know.

|**Process**|**Full Form**|**Purpose**|**SOC Importance**|
|---|---|---|---|
|**smss.exe**|Session Manager Subsystem|First user-mode process started by the Windows kernel. Creates user sessions and starts essential system processes.|If missing, duplicated, or running from an unusual path, it may indicate malware.|
|**wininit.exe**|Windows Initialization Process|Starts critical Windows processes such as **services.exe**, **lsass.exe**, and **lsm.exe** during system startup.|A fake or unexpected `wininit.exe` process is highly suspicious.|
|**services.exe**|Service Control Manager (SCM)|Starts, stops, and manages Windows services.|Attackers may create malicious services for persistence.|
|**lsass.exe**|Local Security Authority Subsystem Service|Handles user authentication, password verification, security policies, and stores authentication credentials.|Frequently targeted by tools like **Mimikatz** to dump credentials.|
|**svchost.exe**|Service Host|Hosts one or more Windows services that run from DLL files. Multiple instances normally run simultaneously.|Malware often disguises itself as `svchost.exe`, so analysts verify its location, parent process, and behavior.|

- **smss.exe** → **Starts sessions**
- **wininit.exe** → **Starts Windows core processes**
- **services.exe** → **Manages Windows services**
- **lsass.exe** → **Handles logins and credentials**
- **svchost.exe** → **Hosts Windows services**

```
Windows Kernel
      │
      ▼
smss.exe
      │
      ▼
wininit.exe
      │
      ├────────► services.exe
      ├────────► lsass.exe
      └────────► lsm.exe
                    │
                    ▼
              svchost.exe (Multiple Instances)
                    │
                    ▼
             Windows Services
```


#### Windows Authentication Flow

```
User Login
     │
     ▼
LSASS (Checks Username & Password)
     │
     ▼
Authentication Successful
     │
     ▼
Access Token Created
     │
     ▼
User Gets Access to System Resources
```

1. **User Login**
- The user enters a username and password.

2. **LSASS**
- **LSASS (Local Security Authority Subsystem Service)** verifies the user's credentials.

3. **Authentication**
- If the credentials are correct, Windows authenticates the user.

4. **Access Token**
- Windows creates an **Access Token** for the user.
- The access token is attached to every process the user starts.

##### What is an Access Token?

An Access Token is a security object created after a successful login that contains the user's identity and permissions. Windows uses it to decide what resources the user is allowed to access.

- User Identity (User SID)
- Group Memberships
- User Privileges
- Access Permissions - Determines what files, folders, and applications the user can access.

---

# Windows Registry

The **Windows Registry** is a **central hierarchical database** that stores configuration settings and options for the Windows operating system, hardware, software, users, and system services.

- Stores Windows OS settings.
- Stores application settings.
- Stores hardware configurations.
- Stores user preferences.
- Stores startup information.
- Stores system policies.
- Helps Windows boot and operate correctly.

```
                       Root (Computer)
                             │
                             ▼
                           Hives
                             │
   ┌────────────┬────────────┬────────────┬────────────┐
   ▼            ▼            ▼            ▼            ▼
 HKCR         HKCU         HKLM         HKU         HKCC
   │            │            │            │            │
   └────────────┴────────────┴────────────┴────────────┘
                             │
                             ▼
                           Keys
                             │
                             ▼
                          Subkeys
                             │
                             ▼
                           Values
                             │
        ┌────────────┬────────────┬────────────┐
        ▼            ▼            ▼            ▼
      String       DWORD        QWORD        Binary
```

#### Hives

A Registry Hive is a main section of the Windows Registry that stores configuration related settings for Windows, users, hardware, and applications.

|**Hive**|**Full Name**|**Purpose**|
|---|---|---|
|**HKCR**|HKEY_CLASSES_ROOT|Stores file associations and COM object settings.|
|**HKCU**|HKEY_CURRENT_USER|Stores settings for the currently logged-in user.|
|**HKLM**|HKEY_LOCAL_MACHINE|Stores system-wide settings, hardware, drivers, and installed software.|
|**HKU**|HKEY_USERS|Stores settings for all user accounts on the computer.|
|**HKCC**|HKEY_CURRENT_CONFIG|Stores the current hardware configuration.|

- REG_SZ -> Strings
- REG_DWORD -> Numbers
- REG_BINARY -> Binary

### Registry & Attacks

#### 1. WMI Persistence

WMI Persistence is an advanced persistence technique that uses Windows Management Instrumentation (WMI) to automatically run malware without adding it to common startup locations.

- Allowing malware to remain active even after a reboot.

##### Example

- Malware creates a WMI event.
- Every time a user logs in, the WMI event triggers.
- PowerShell or another malicious program runs automatically.

#### 2. Registry Hijacking

Registry Hijacking is the modification of Windows Registry entries to make Windows run a malicious program instead of the legitimate one.

##### Example

Instead of:

```
C:\Windows\System32\notepad.exe
```

the attacker changes the Registry to:

```
C:\Users\Admin\AppData\Temp\malware.exe
```

## SOC Detection – What to Monitor

- Suspicious Registry Entries - `poweshell.exe in Run key`
- Unknown Executables - `abc123.exe`
- Unusual Paths - `C:\ProgramData\`

