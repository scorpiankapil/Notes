# The 3 SOC Operating Models

Organizations usually run a SOC in 3 common ways depending on:

- budget,
- company size,
- security maturity,
- and staffing.

# **1. In-House (Internal) SOC** 

An In-House SOC (Security Operations Center) is a cybersecurity monitoring and defense team that is built, managed, and operated inside an organization by its own employees instead of outsourcing security monitoring to another company.

The organization creates its own SOC room/team to continuously monitor systems, networks, servers, endpoints, logs, and security alerts.

## Typical In-House SOC Team Structure 

|Role|Work|
|---|---|
|SOC Analyst L1|Monitor alerts and triage|
|SOC Analyst L2|Deep investigation|
|SOC Analyst L3|Advanced threat hunting & malware analysis|
|Incident Responder|Handle security incidents|
|SOC Manager|Manage SOC operations|
|Threat Hunter|Search hidden threats|
|SIEM Engineer|Configure SIEM tools|
### Example

A large bank creates its own SOC team with:

- SIEM
- SOC analysts
- Threat hunters
- Incident responders

### Advantages

- Full control over security
- Faster internal communication
- Better understanding of company environment
- Sensitive data stays internal

### Disadvantages

- Expensive
- Requires skilled staff
- 24/7 monitoring is difficult
- High maintenance cost

### Best For

- Large enterprises
- Banks
- Government organizations
- Big tech companies


# **2. Outsourced / Managed SOC (MSP/MSSP SOC)**

An Outsourced SOC or Managed SOC is a Security Operations Center that is handled by an external cybersecurity company instead of the organization building and managing its own internal SOC team.

These external companies are called:

MSP → Managed Service Provider
MSSP → Managed Security Service Provider

An MSSP specializes specifically in cybersecurity monitoring and defense.

### Example

A startup hires:

- Secureworks
- CrowdStrike
- Rapid7

to monitor their environment.

### Advantages

- Lower cost
- No need to hire large teams
- 24/7 monitoring available
- Quick deployment

### Disadvantages

- Less control
- Slower communication sometimes
- Third party handles sensitive logs
- Analysts may not fully understand business context

### Best For

- Small businesses
- Startups
- Companies with limited budget

### Key Difference in MSP & MSSP

| Core Point             | MSP                                 | MSSP                              |
| ---------------------- | ----------------------------------- | --------------------------------- |
| Full Form              | Managed Service Provider            | Managed Security Service Provider |
| Core Work              | Manages IT infrastructure           | Manages cybersecurity             |
| Main Goal              | Keep systems running                | Keep systems secure               |
| Focus Area             | IT operations                       | Security operations               |
| Handles Cyber Threats? | Not mainly                          | Yes                               |
| Monitors               | Servers, networks, backups, systems | Security alerts, attacks, threats |
| SOC Operations         | Usually No                          | Yes                               |
| Incident Response      | IT issue fixing                     | Cyber attack response             |
| Security Expertise     | Basic IT security                   | Advanced cybersecurity            |
| Example Problem Solved | “Server is down”                    | “Ransomware detected”             |
| Main Tools             | Remote management, backup tools     | SIEM, EDR, IDS/IPS, SOAR          |
| Main Responsibility    | Availability & performance          | Threat detection & protection     |

# **3. Hybrid SOC (Co-Managed SOC)**

A Hybrid SOC or Co-Managed SOC is a combination of both:

In-House SOC
Outsourced/Managed SOC (MSSP)

In this model, the organization’s internal security team works together with an external MSSP provider to manage cybersecurity operations.

## Why Companies Use Hybrid SOC

Many organizations:

- Want internal control
- But also need 24/7 monitoring and expert support

So they combine both models.

- Internal team handles critical incidents
- External MSSP handles monitoring and initial triage

This gives:

- Better coverage
- Lower cost than full in-house SOC
- More control than full outsourcing

### Advantages

- Balanced cost
- Better coverage
- Internal control + external expertise
- Easier 24/7 operations

### Disadvantages

- Coordination can be complex
- Requires good communication
- Shared responsibility issues

### Best For

- Medium to large companies
- Growing organizations
- Enterprises scaling security operations

# System As Attack Vector

When we say “System as an attack vector”, it means the system itself becomes the medium or entry point used by attackers to compromise other systems, users, or networks.

### Real Example

Imagine:

- Employee laptop gets infected with malware.
- Attacker gains access.
- That laptop is now used to:
    - scan internal network,
    - steal credentials,
    - attack servers,
    - send phishing emails.

Now that laptop itself is an **attack vector.**

### A system becomes an attack vector when an attacker uses it to:

- Gain initial access
- Move laterally (One system to another) 
- Maintain persistence (Stay inside the system for long time)
- Exfiltrate data (Steal data and send outside the network)
- Launch Further Attacks  (Compromised systems are often used to attack other system or organizations).

# Human Oriented Attacks

Human-oriented attacks are cyberattacks that target people instead of systems directly.

Instead of hacking software first, attackers try to:

- manipulate humans,
- trick employees,
- steal credentials,
- or convince users to perform unsafe actions.

This is also called Social Engineering

### Common Causes

- Plugging unknown USB devices
- Downloading pirated software
- Clicking suspicious links
- Opening malicious attachments
- Reusing weak passwords
- Trusting fake people/websites
- Using outdated software

### Examples

1. Malicious USB / Rubber Ducky
2. Keyloggers with Software
3. Phishing Links
4. Malicious Attachments (in mail box)
5. Weak Password Reuse

### Prevention Methods

- Security awareness training
- Multi-Factor Authentication (MFA)
- Strong passwords
- Email filtering
- Avoid pirated software
- Verify links before clicking
- Keep software updated


# Supply Chain Attacks

A Supply Chain Attack is a cyberattack where attackers compromise a trusted third-party vendor, software, service, or supplier to indirectly attack the target organization.

Instead of attacking the target directly, attackers compromise something the target already trusts.

### Why Attackers Use Supply Chain Attacks

Organizations trust:

- Software vendors
- Cloud providers
- Hardware manufacturers
- IT service providers
- Third-party libraries

Attackers abuse this trust to spread malware or gain access more easily.

### How Supply Chain Attacks Work

1. Attackers compromise a trusted third-party vendor or software provider.
2. Malicious code or malware is inserted into trusted software or updates.
3. Victims unknowingly download and install the infected software.
4. The malware executes and gives attackers access to the organization.
5. Attackers steal data, spread malware, or compromise the network further.

# Vulnerability

A vulnerability is a weakness, flaw, or security gap in a system, software, network, or human process that attackers can exploit to gain unauthorized access or cause damage.

# Software Vulnerabilities

Software vulnerabilities are weaknesses, bugs, or flaws in software applications that attackers can exploit to gain unauthorized access, execute malicious code, steal data, or disrupt systems.
### Examples of Software Vulnerabilities

- SQL Injection
- Command Injection
- Buffer Overflow
- Cross-Site Scripting (XSS)
- Remote Code Execution (RCE)

### SOC Alerts/Detection

- WAF alerts
- Web server logs
- Unusual POST requests
- EDR alerts on servers

# Network Vulnerabilities

Network vulnerabilities are weaknesses or security flaws in a network that attackers can exploit to gain unauthorized access, steal data, disrupt services, or spread malware.

### Examples of Network Vulnerabilities

- Open ports
- Weak Protocols (Telnet, FTP)
- Unsecured Wi-Fi networks
- Default router credentials
- Unpatched network devices
- Insecure protocols (Telnet, FTP, HTTP)
- Misconfigured firewalls
- Weak network segmentation

### SOC Detection

- IDS/IPS alerts
- Firewall logs
- Unusual inbound/outbound traffic
- Port scanning activity
- Suspicious network connections
- Brute-force login attempts
- Abnormal bandwidth usage
- Unauthorized device connections


# Operating System Vulnerabilities

Operating system vulnerabilities are security weaknesses or flaws present in an operating system that attackers can exploit to gain unauthorized access, execute malicious code, steal data, or disrupt system operations.

These vulnerabilities may exist in:

- System files
- Kernel
- Services
- Permissions
- Configurations
- Built-in applications

### Examples of Operating System Vulnerabilities

- Unpatched operating systems
- Weak user permissions
- Privilege escalation flaws
- Default system configurations
- Weak password policies
- Outdated kernel versions
- Insecure services enabled
- Missing security updates

### SOC Detection

- Failed login attempts
- Privilege escalation alerts
- Suspicious system processes
- Unauthorized admin access
- EDR alerts on endpoints
- Abnormal system behavior
- Exploit detection alerts
- Security event logs analysis

# Authentication & Authorization Vulnerabilities

## Authentication Vulnerability

 An authentication vulnerability is a security weakness in the identity verification process that allows attackers to bypass login mechanisms or gain unauthorized access to a system.

### Examples of Authentication Vulnerabilities

- Weak passwords
- Default credentials
- Missing Multi-Factor Authentication (MFA)
- Brute-force vulnerable login pages
- Credential stuffing attacks
- Session fixation
- Insecure password reset mechanisms
- Poor session management

## Authorization Vulnerability

 An authorization vulnerability is a security weakness in access control mechanisms that allows users to access resources, data, or actions beyond their permitted privileges.

### Examples of Authorization Vulnerabilities

- Privilege escalation
- Broken Access Control
- IDOR (Insecure Direct Object Reference)
- Accessing admin pages without permission
- Horizontal privilege escalation
- Vertical privilege escalation
- Excessive user permissions
- Improper role-based access control

### SOC Detection

- Multiple failed login attempts
- Login from unusual locations
- Unauthorized admin access
- Suspicious session activity
- Account lockout alerts
- Privilege escalation alerts
- Access to restricted resources
- Abnormal user behavior logs

# Configuration-Dependent Vulnerabilities

Configuration-dependent vulnerabilities are security weaknesses that occur because of improper, insecure, or default system configurations instead of flaws in the software itself.

These vulnerabilities appear when systems, applications, servers, or network devices are not configured securely.

#### Examples of Configuration-Dependent Vulnerabilities

- Default usernames and passwords
- Misconfigured firewalls
- Open unnecessary ports
- Publicly exposed cloud storage
- Directory listing enabled
- Improper access permissions
- Debug mode enabled in production
- Unsecured database configurations
- Weak security policies
- Disabled security controls

### SOC Detection

- Firewall configuration alerts
- Exposure scanning results
- Unauthorized access attempts
- Open port detection
- Cloud security alerts
- Abnormal configuration changes
- SIEM correlation alerts
- Security audit log analysis

# Zero-Day Vulnerabilities

A zero-day vulnerability is a security flaw in software, hardware, or an operating system that is unknown to the vendor or has no available patch or fix at the time it is discovered or exploited.

Attackers exploit the vulnerability before developers can fix it.

It is called “zero-day” because:

- The vendor has had zero days to fix the vulnerability.
- No official patch or protection is available initially

### Why Zero-Day Vulnerabilities Are Dangerous

- No immediate fix available
- Hard to detect initially
- Antivirus may not recognize the exploit
- Attackers can secretly exploit systems for a long time

### Lifecycle of a Zero-Day Vulnerability

1. A new vulnerability is discovered in software or a system.
2. Attackers develop a method or exploit to use the vulnerability.
3. Cybercriminals exploit the vulnerability to perform attacks and cause damage.
4. The software vendor discovers and analyzes the vulnerability.
5. The vendor releases a security patch or update to fix the vulnerability.

# **Common Misconfiguration for SOC** 

# Cloud Misconfiguration

Cloud misconfiguration is a security weakness caused by incorrect or insecure settings in cloud services, storage, servers, networks, or permissions that expose systems and data to unauthorized access.

- Public S3 Buckets
- Open Azure Blob storage
- Over-permissive IAM roles
- Exposed access keys

# Network Misconfiguration

Network misconfiguration is a security weakness caused by incorrect or insecure network settings that expose systems, devices, or data to unauthorized access and cyber attacks.

- Firewall allow all traffic
- Internal services exposed externally
- No network segmentation (All devices on same network)
- Weak Wi-Fi security

# Identity Misconfiguration

Identity misconfiguration is a security weakness caused by improper identity and access management (IAM) settings that allow unauthorized users to access systems, accounts, or resources.

- Disabled multi-factor authentication (MFA)
- Excessive group membership
- Shared admin and user accounts
- Misconfigured IAM roles
- Unused accounts left active

# Endpoint Misconfiguration

Endpoint misconfiguration is a security weakness caused by incorrect or insecure settings on endpoint devices such as laptops, desktops, mobile devices, or servers.

- Disabled antivirus or firewall
- Weak password settings
- Unpatched operating systems
- Unsecured remote desktop access
- USB allowed everywhere
- Local admin access
- Outdated software