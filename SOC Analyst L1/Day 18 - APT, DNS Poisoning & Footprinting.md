# DNS Footprinting

**DNS Footprinting** is the process of gathering information about a target domain by querying its DNS records. It helps identify hosts, servers, IP addresses, mail servers, and other network information.

- Discover IP addresses.
- Identify subdomains.
- Find mail servers.
- Gather DNS records.
- Map the target's network infrastructure.
- Perform reconnaissance before a security assessment.

### Information Collected

- **A Record** → IPv4 address.
- **AAAA Record** → IPv6 address.
- **MX Record** → Mail server.
- **NS Record** → Name server.
- **CNAME Record** → Alias of a domain.
- **TXT Record** → Verification and security information (e.g., SPF, DKIM, DMARC).
- **SOA Record** → Information about the DNS zone.

#### Common DNS Footprinting Tools

- **nslookup**
- **dig**
- **host**
- **dnsenum**
- **dnsrecon**
- **Fierce**
- **Amass**
- **Subfinder**

## DNS Poisoning

DNS Poisoning is a cyberattack in which an attacker inserts false or malicious DNS records into a DNS server or DNS cache, causing users to be redirected to a fake or malicious website instead of the legitimate one.

- DNS Server
- Local router

##### Working of DNS Poisoning

- The attacker compromises a **DNS server** or **DNS cache** by inserting fake DNS records.
- The user enters the correct website address (e.g., www.bank.com) in the browser.
- The DNS server returns a **fake IP address** instead of the legitimate IP address.
- The user's browser automatically connects to the **attacker's fake website**.
- The victim enters sensitive information (such as usernames, passwords, or banking details), which is stolen by the attacker.

##### Simple Example

**Normal Process**

```
User enters: www.bank.com
            ↓
        DNS Server
            ↓
Returns Real IP (192.168.1.10)
            ↓
User visits the Real Bank Website
```

**DNS Poisoning Attack**

```
User enters: www.bank.com
        ↓
Poisoned DNS Server
        ↓
Returns Fake IP (203.0.113.50)
        ↓
User visits Fake Bank Website
        ↓
Enters Username & Password
        ↓
Attacker Steals Credentials
```


# APT (Advance Persistent Threat)

**An Advanced Persistent Threat (APT)** is a sophisticated cyber attack in which attackers gain unauthorized access to a target network and remain hidden for a long time to steal sensitive data, monitor activities, or disrupt operations.

- **Advanced** → Uses advanced hacking techniques and tools.
- **Persistent** → Stays inside the network for a long time without being detected.
- **Threat** → Has malicious intentions, such as stealing data or spying.

```
                 APT Attack Chain

Reconnaissance
       │
       ▼
Initial Access
(Phishing / Exploit / Stolen Credentials)
       │
       ▼
Malware / Backdoor Installation
       │
       ▼
Persistence
(Maintain Long-Term Access)
       │
       ▼
Privilege Escalation
       │
       ▼
Lateral Movement
(Move to Other Systems)
       │
       ▼
Credential Access
(Steal Passwords / Hashes)
       │
       ▼
Discovery
(Find Sensitive Data & Systems)
       │
       ▼
Command & Control (C2)
(Communicate with Attacker)
       │
       ▼
Data Collection
       │
       ▼
Data Exfiltration
(Steal Sensitive Information)
       │
       ▼
Maintain Access / Cover Tracks
```