# What is PowerShell?

**PowerShell** is Microsoft's **command-line shell and scripting language** used to automate tasks, manage Windows systems, and administer computers.

- Run system commands.
- Automate repetitive tasks.
- Manage files and folders.
- Manage Windows services and processes.
- Manage users and permissions.
- Configure network settings.
- Control remote computers.
- Execute PowerShell scripts (`.ps1`).

**Example Commands:**

|**Command**|**Purpose**|
|---|---|
|`Get-Process`|List running processes.|
|`Get-Service`|Show Windows services.|
|`Get-ChildItem`|List files and folders.|
|`Get-Help`|Display help for commands.|
|`Stop-Process`|Stop a running process.|

## Why Attackers love PowerShell

**It can:**
- Execute Commands
- Download payloads
- Access registry
- Modify services
- Execute scripts in memory
- Bypass GUI restrictions

## PowerShell in Cybersecurity

PowerShell is a **legitimate administration tool**, but it is also commonly abused by attackers.

| **For Defenders (SOC / IR)**                                         | **For Attackers**                                                              |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Automates incident response and forensic collection.                 | Executes fileless malware directly in memory.                                  |
| Performs threat hunting and system auditing.                         | Enables lateral movement and privilege escalation.                             |
| Integrates with SIEM tools (e.g., Microsoft Sentinel, Splunk).       | Uses obfuscated or Base64-encoded commands to evade detection.                 |
| Automates security and remediation tasks through scripted playbooks. | Uses Living-off-the-Land (LOLBins) techniques to abuse built-in Windows tools. |

## Security Best Practices

- Enable **PowerShell Logging** (Script Block Logging, Module Logging, Transcription).
- Restrict PowerShell Remoting to authorized administrators.
- Monitor for encoded or obfuscated commands.
- Apply least privilege and keep Windows updated.

## PowerShell and CMD (Command Prompt)

| **PowerShell**                                                             | **CMD (Command Prompt)**                                        |
| -------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Uses **.NET objects** as output.                                           | Uses **plain text** as output.                                  |
| Supports `.ps1` scripting.                                                 | Supports `.bat` and `.cmd` batch files.                         |
| Designed for **automation and system administration**.                     | Designed for **basic command execution**.                       |
| Can manage **services, registry, users, processes, and Active Directory**. | Limited to basic Windows commands and file operations.          |
| Supports **remote management** (PowerShell Remoting).                      | No built-in remote management.                                  |
| More **powerful and feature-rich**.                                        | Simpler and easier for basic tasks.                             |
| Commonly used by **System Administrators, SOC Analysts, and Pentesters**.  | Commonly used for **basic troubleshooting and legacy scripts**. |
| Example: `Get-Process`, `Get-Service`, `Get-ChildItem`                     | Example: `tasklist`, `sc query`, `dir`                          |

## How PowerShell Works

1. User enters a command.
2. PowerShell Engine parses the command.
3. The appropriate cmdlet or script is executed.
4. Cmdlets use the .NET Framework/.NET Runtime.
5. .NET communicates with Windows APIs.
6. Windows performs the requested operation.
7. Results are returned as **objects**.
8. PowerShell displays the output to the user.