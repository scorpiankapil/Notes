# Windows Architecture

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