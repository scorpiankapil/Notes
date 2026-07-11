# SOC L1 Readiness Test (Sections A, B, C & D)

## Section A - Multiple Choice Questions (25)

1. What is the primary role of a SOC L1 analyst?
A. Develop malware
B. Monitor alerts and perform initial triage✅
C. Write security policies
D. Perform penetration testing

2. Which malware encrypts files and demands payment?
A. Trojan
B. Worm
C. Ransomware✅
D. Spyware
 
3. Which attack uses one password across many accounts?
A. Brute Force
B. Dictionary Attack
C. Password Spraying✅
D. Credential Stuffing

4. What does hashing primarily provide?
A. Confidentiality
B. Integrity✅
C. Authentication
D. Availability

5. What does salting prevent?
A. Brute force attacks
B. Rainbow table attacks✅
C. Phishing
D. DDoS

6. Which tool is commonly used for credential dumping?
A. Wireshark
B. Metasploit
C. Mimikatz✅
D. Burp Suite

7. Which Windows process stores authentication credentials?
A. svchost.exe
B. explorer.exe
C. lsass.exe✅
D. winlogon.exe

8. Which attack redirects users to a fake website without clicking a malicious link?
A. Phishing
B. Pharming✅
C. Smishing
D. Baiting

9. Moving between compromised systems inside a network is called?
A. Privilege escalation
B. Persistence
C. Lateral movement✅
D. Data exfiltration

10. Which encryption type uses two keys?
A. Symmetric
B. Asymmetric✅
C. Hashing
D. Encoding

11. Fraudulent emails to steal credentials represent which attack?
A. Phishing✅
B. Malware
C. DDoS
D. SQL Injection

12. What does IOC stand for?
A. Indicator of Compromise✅
B. Incident of Crime
C. Internal Operations Control
D. Internet Operations Center

13. Which attack uses leaked credentials from previous breaches?
A. Brute force
B. Credential stuffing✅
C. Password spraying
D. Dictionary

14. Which attack floods servers with traffic?
A. Malware
B. Phishing
C. DDoS✅
D. Brute Force

15. Which technique extracts credentials from system memory?
A. Credential dumping✅
B. Encryption
C. Hash collision
D. Tokenization

16. Targeted phishing aimed at a specific individual is called?
A. Phishing
B. Spear phishing✅
C. Smishing
D. Vishing

17. What does SIEM primarily do?
A. Develop malware
B. Log collection and analysis✅
C. Replace antivirus
D. Disable attacks

18. Which security principle ensures data is unchanged?
A. Confidentiality
B. Integrity✅
C. Availability
D. Authentication

19. Which protocol is used for remote Windows access?
A. FTP
B. RDP✅
C. SMTP
D. DNS

20. Which authentication uses multiple verification factors?
A. Single factor
B. MFA✅
C. Password only
D. Tokenization

21. What is alert triage?
A. Ignoring alerts
B. Investigating and prioritizing alerts✅
C. Deleting logs
D. Disabling SIEM

22. Privilege escalation from user to admin is called?
A. Horizontal
B. Vertical✅
C. Passive
D. Internal

23. Event ID 4625 represents?
A. Successful login
B. Failed login✅
C. Account deletion
D. Password reset

24. Fake Wi-Fi network attack is called?
A. Evil Twin✅
B. Pharming
C. Smishing
D. Tailgating

25. Which SOC process analyzes alerts to determine threats?
A. Alert triage✅
B. Encryption
C. Backup
D. Patch management

## Section B - Short Answer Questions

#### 1. Explain the difference between hashing and encryption.

Hashing is a one-way process used for integrity verification. Encryption is a two-way process used for confidentiality, where data can be decrypted using the correct key.

#### 2. What is password spraying and why is it difficult to detect?

- Uses **one or a few common passwords** across many accounts.
- **Avoids repeated login attempts** on a single account, reducing the chance of triggering account lockouts.
- Login attempts are **spread over multiple users** and often over a longer time period.
- Can appear similar to **normal failed login activity** in large organizations.
- Attackers often use **multiple IP addresses** or **slow attack rates**, making detection more difficult.

#### 3. What is lateral movement and why do attackers perform it?

**Lateral movement** is a post-exploitation technique in which an attacker moves from one compromised system to other systems within the same network. Attackers perform lateral movement to expand their access, locate valuable data, compromise additional devices, obtain higher privileges, and eventually reach critical systems such as domain controllers or file servers. This technique helps attackers achieve their objectives while maintaining persistence and increasing the impact of the attack.

#### 4. Explain vertical vs horizontal privilege escalation.

**Vertical privilege escalation** occurs when an attacker increases their access rights by moving from a **lower-privileged account to a higher-privileged account**, such as from a normal user to an administrator or root account. The goal is to gain elevated permissions to perform restricted actions, access sensitive data, or take full control of the system.

**Horizontal privilege escalation** occurs when an attacker accesses the resources or data of **another user with the same privilege level** without increasing their permissions. For example, one standard user accessing another standard user's account or files. The goal is to gain unauthorized access to another user's information while remaining at the same privilege level.

#### 5. What is credential stuffing?

**Credential stuffing** is a type of cyberattack in which an attacker uses **stolen usernames and passwords from previous data breaches** to attempt logins on multiple websites and online services. It is effective because many users reuse the same password across different accounts. If the stolen credentials work on another service, the attacker gains unauthorized access without needing to guess or crack the password.

Organizations can reduce the risk of credential stuffing by encouraging unique passwords, enabling **multi-factor authentication (MFA)**, and monitoring for suspicious login attempts.

#### 6. Explain the concept of salting in password storage.

**Salting** is the process of adding a **unique random value (called a salt)** to a password before hashing it. This ensures that even if two users have the same password, their hashed passwords will be different. Salting protects stored passwords from **rainbow table attacks** and makes password cracking much more difficult. Each user should have a unique salt stored along with their hashed password, improving the overall security of password storage.

#### 7. What are Indicators of Compromise (IOC)? Give examples.

**Indicators of Compromise (IOCs)** are **pieces of evidence that indicate a system or network may have been compromised by a cyberattack**. Security teams use IOCs to detect, investigate, and respond to malicious activities. Common examples include **malicious IP addresses, suspicious domain names, file hashes (MD5/SHA-256), unusual login attempts, unexpected processes, registry changes, and abnormal network traffic**. Identifying IOCs helps organizations detect threats early and reduce the impact of security incidents.

#### 8. Explain the difference between phishing and spear phishing.

**Phishing** is a cyberattack in which attackers send **generic fraudulent emails, messages, or websites** to a large number of people to steal sensitive information such as usernames, passwords, or banking details. The attack is not targeted at any specific individual.

**Spear phishing** is a **targeted form of phishing** in which attackers customize the message for a specific person or organization using personal or professional information. Because the message appears more legitimate and relevant, spear phishing has a much higher success rate.

#### 9. What is an Evil Twin attack?

**An Evil Twin attack** is a type of **Wi-Fi attack** in which an attacker creates a **fake wireless access point** that looks identical to a legitimate Wi-Fi network. Unsuspecting users connect to the fake network, believing it is genuine. Once connected, the attacker can intercept network traffic, steal sensitive information such as usernames and passwords, monitor user activity, or redirect victims to malicious websites. Evil Twin attacks are commonly performed in public places like cafés, airports, and hotels where free Wi-Fi is available.

#### 10. What is alert triage in SOC operations?

**Alert triage** is the process of **reviewing, analyzing, and prioritizing security alerts** generated by security tools such as a SIEM or EDR. SOC analysts examine each alert to determine whether it is a **true positive, false positive, or a potential security incident**. Based on the severity and impact, they prioritize alerts for further investigation or response, ensuring that critical threats are addressed quickly while reducing unnecessary workload from false alarms.

## Section C - Scenario Based Questions

### 1. Logs show 500 failed login attempts from the same IP targeting one account.

The logs show **500 failed login attempts from the same IP address targeting a single user account**, which is a strong indicator of a **brute force attack**. In a brute force attack, the attacker repeatedly tries different passwords on one account until the correct password is found. This behavior is often detected by a high number of failed login attempts from the same source in a short period and may trigger account lockout or security alerts.

### 2. One password attempted across 200 user accounts.

The logs show **one common password being attempted across 200 different user accounts**, which is a clear indicator of a **password spraying attack**. Instead of trying many passwords on a single account, the attacker uses the same password against multiple accounts to avoid triggering account lockout policies. This technique is effective because many users choose weak or common passwords, making the attack harder to detect.

### 3. Mimikatz executed, LSASS accessed, admin login occurs, RDP to file server.

The attacker first uses **Mimikatz** to access the **LSASS** process and dump stored credentials (**Credential Dumping**). The stolen credentials are then used to gain **administrator privileges** (**Privilege Escalation**). Finally, the attacker uses **RDP** to access the file server, moving from the compromised system to another system within the network (**Lateral Movement**). This attack chain is commonly seen during post-exploitation to gain broader access and compromise critical resources.

```
Credential Dumping → Privilege Escalation → Lateral Movement
```

### 4. Employee receives email: 'Your account will be suspended. Click here to reset password.'

The email is a classic **phishing attack** because it uses an urgent message ("Your account will be suspended") to trick the employee into clicking a malicious link and entering their login credentials. The attacker aims to steal sensitive information such as usernames and passwords by impersonating a trusted organization.

### 5. Login from India followed by login from Russia within 3 minutes.

The logs show a login from **India** followed by another login from **Russia** within **3 minutes**, which is physically impossible for a legitimate user. This is known as **impossible travel / Suspicious Login Activity** and may indicate that the user's account has been compromised or that stolen credentials are being used from different locations. Such events should be investigated immediately by the SOC team.

## Section D - Analyst Thinking

### 1. What steps would you take when investigating a suspicious login alert?

- Check the source IP address.
- Verify the geolocation of the login.
- Review the user's login behavior and history.
- Check the device information (device ID/browser/OS).
- Verify the login time for unusual activity (e.g., impossible travel).
- Analyze authentication logs for failed and successful login attempts.
- Determine whether the login is legitimate or suspicious.
- If malicious, reset the password, terminate active sessions, and escalate the incident.

### 2. If a user clicked a phishing email, what should the SOC analyst do first?

- Isolate the affected system from the network.
- Reset the user's password and revoke active sessions.
- Check for malware or malicious activity.
- Analyze email, endpoint, and authentication logs.
- Block the malicious URL, domain, or sender.
- Escalate the incident to the Incident Response team.
- Monitor the account and system for further suspicious activity.

### 3. Why do attackers try to escalate privileges after gaining initial access?

Attackers try to **escalate privileges** after gaining initial access because **higher privileges allow them to disable security controls, access sensitive data and critical systems, move laterally across the network, maintain persistence, and gain full control of the compromised environment.**

### 4. How would you differentiate between a false positive and a real incident?

To differentiate between a **false positive** and a **real incident**, **correlate logs from multiple sources, check the context of the alert, analyze user behavior, validate the activity against normal patterns, and look for supporting evidence of malicious actions.** If the activity is legitimate, it is a **false positive**; if it indicates unauthorized or malicious behavior, it is a **real security incident**.

### 5. What logs would you check when investigating a brute force attack?

When investigating a **brute force attack**, check the **Windows Security Logs** (e.g., Event IDs **4625** for failed logins and **4624** for successful logins), **authentication logs**, **VPN logs**, **firewall logs**, **Active Directory logs**, and **SIEM alerts**. These logs help identify the source IP address, number of failed login attempts, targeted accounts, login patterns, and any successful compromise after repeated failures.

---

# SOC L1 Log Investigation Practical Test

# Scenario 1 — Authentication Log Analysis

### SIEM Alert

- **Alert Name:** Multiple Failed Login Attempts
- **Source IP:** 185.221.10.45
- **Target User:** administrator
- **Event ID:** 4625
- **Attempts:** 320
- **Time Window:** 4 minutes

### Q1. What type of attack is likely occurring?

A. Credential Stuffing  
**B. Brute Force Attack ✅**  
C. Phishing  
D. SQL Injection

**Answer:** Brute Force Attack

---

### Q2. Which log field indicates the attacker's source?

A. Account Name  
**B. Source Network Address ✅**  
C. Event ID  
D. Logon Type

**Answer:** Source Network Address

---

### Q3. What does Event ID 4625 represent?

A. Successful Login  
**B. Failed Login Attempt ✅**  
C. Account Created  
D. Password Changed

**Answer:** Failed Login Attempt

---

### Q4. What should the SOC analyst check next?

**A. Successful login events (4624) ✅**  
B. Email logs  
C. Firewall firmware  
D. DNS records

**Answer:** Successful Login Events (4624)

---

# Scenario 2 — Suspicious Login Alert

### SIEM Alert

- **User:** john.doe
- **Previous Login:** India
- **New Login:** Russia
- **Time Difference:** 2 minutes
- **Authentication:** O365

### Q5. What security indicator does this represent?

**A. Impossible Travel ✅**  
B. Phishing  
C. Malware  
D. Data Exfiltration

**Answer:** Impossible Travel

---

### Q6. What attack might have happened before this login?

**A. Phishing or Credential Theft ✅**  
B. Hardware Failure  
C. DNS Misconfiguration  
D. Software Update

**Answer:** Phishing or Credential Theft

---

### Q7. What should the SOC analyst check immediately?

**A. Login History and IP Reputation ✅**  
B. CPU Temperature  
C. Printer Logs  
D. Monitor Resolution

**Answer:** Login History and IP Reputation

---

### Q8. What immediate response action should be taken?

A. Ignore Alert  
**B. Force Password Reset and Revoke Sessions ✅**  
C. Restart Router  
D. Delete User Account

**Answer:** Force Password Reset and Revoke Sessions

---

# Scenario 3 — Email Security Alert

### Email Gateway Alert

- **Sender:** security-update@micros0ft-support.com
- **Recipient:** hr@company.com
- **Attachment:** Salary_Adjustment_2025.xlsm
- **SPF:** Fail
- **DKIM:** Fail
- **DMARC:** Fail

### Q9. What type of attack is this?

**A. Phishing ✅**  
B. Ransomware  
C. DDoS  
D. Brute Force

**Answer:** Phishing

---

### Q10. Which indicator suggests the email is malicious?

**A. SPF/DKIM/DMARC Failures ✅**  
B. Correct Grammar  
C. Known Sender  
D. Internal Email

**Answer:** SPF/DKIM/DMARC Failures

---

### Q11. What risk does the .xlsm attachment indicate?

A. Image File  
**B. Macro-based Malware ✅**  
C. Video File  
D. Audio File

**Answer:** Macro-based Malware

---

### Q12. What should SOC do if the user opened the attachment?

A. Ignore Alert  
**B. Isolate Endpoint and Scan System ✅**  
C. Delete Email Only  
D. Disable Wi-Fi

**Answer:** Isolate Endpoint and Scan System

---

# Scenario 4 — Endpoint Security Alert

### EDR Alert

- **Host:** HR-Laptop-14
- **Process:** mimikatz.exe
- **Target Process:** lsass.exe

### Q13. What attack technique is being used?

**A. Credential Dumping ✅**  
B. SQL Injection  
C. Cross-Site Scripting  
D. DDoS

**Answer:** Credential Dumping

---

### Q14. What sensitive data is the attacker trying to extract?

**A. Password Hashes and Kerberos Tickets ✅**  
B. Images  
C. Video Files  
D. Printer Drivers

**Answer:** Password Hashes and Kerberos Tickets

---

### Q15. Which Windows process stores authentication credentials?

A. explorer.exe  
**B. lsass.exe ✅**  
C. notepad.exe  
D. chrome.exe

**Answer:** lsass.exe

---

### Q16. What attack stages may follow this activity?

**A. Privilege Escalation and Lateral Movement ✅**  
B. Backup Operation  
C. Software Update  
D. System Reboot

**Answer:** Privilege Escalation and Lateral Movement

---

# Scenario 5 — Lateral Movement Alert

### SIEM Alert

- **Source Host:** HR-Laptop-14
- **Destination Host:** FileServer-02
- **Protocol:** RDP
- **User:** Administrator
- **Time:** 03:12 AM

### Q17. What attack phase does this indicate?

**A. Lateral Movement ✅**  
B. Phishing  
C. Data Backup  
D. System Patch

**Answer:** Lateral Movement

---

### Q18. Why is this login suspicious?

**A. Admin Account Used from User Workstation ✅**  
B. Normal Business Activity  
C. Scheduled Task  
D. System Update

**Answer:** Admin Account Used from User Workstation

---

### Q19. What previous attack likely enabled this?

**A. Credential Dumping or Phishing ✅**  
B. Hardware Failure  
C. DNS Update  
D. Antivirus Scan

**Answer:** Credential Dumping or Phishing

---

### Q20. What logs should SOC investigate next?

**A. Windows Security Logs ✅**  
B. Music Files  
C. Printer Logs  
D. Monitor Settings

**Answer:** Windows Security Logs

---

# Scenario 6 — Data Exfiltration Alert

### Firewall Log

- **Source IP:** 192.168.10.15
- **Destination IP:** 45.77.123.66
- **Protocol:** HTTPS
- **Data Transfer:** 4.8 GB
- **Time:** 02:41 AM
- **Host:** Finance-PC-03

### Q21. What suspicious activity could this represent?

**A. Data Exfiltration ✅**  
B. Software Update  
C. Backup Process  
D. Antivirus Scan

**Answer:** Data Exfiltration

---

### Q22. Why is the time of activity important?

**A. Occurred Outside Normal Business Hours ✅**  
B. System Reboot  
C. Hardware Check  
D. Printer Job

**Answer:** Occurred Outside Normal Business Hours

---

### Q23. What should the SOC analyst investigate next?

**A. File Access Logs and User Activity ✅**  
B. Screen Brightness  
C. Mouse Driver  
D. Keyboard Settings

**Answer:** File Access Logs and User Activity

---

### Q24. What type of incident might this become?

**A. Data Breach ✅**  
B. Hardware Issue  
C. Printer Failure  
D. Software Update

**Answer:** Data Breach