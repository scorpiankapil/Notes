# Man-in-the-Middle (MITM) Attack

A Man-in-the-Middle (MITM) Attack is a cyberattack in which an attacker secretly intercepts, monitors, and may alter the communication between two parties without their knowledge.

```
Victim
   │
   ▼
Attacker (MITM)
   │
   ▼
Website / Server
```

### Goal of MITM 

- Steal credentials
- Capture session cookies
- Modify data in transit
- Inject malware
- Monitor sensitive communication

## Types of MITM Attacks

## 1. ARP Spoofing

**ARP Spoofing (ARP Poisoning)** is an attack where an attacker sends **fake ARP (Address Resolution Protocol) messages** on a local network to trick devices into associating the attacker's **MAC address** with the IP address of another device (usually the router).

As a result, **all network traffic passes through the attacker's system**, allowing them to intercept, monitor, or modify the data.

ARP Spoofing is a MITM attack in which an attacker sends fake ARP replies to make victims believe the attacker's device is the router, causing network traffic to flow through the attacker.

#### How ARP Spoofing works?

- **Victim wants to communicate with the router.**
- **Victim sends an ARP request** asking for the router's MAC address.
- **Attacker joins the same local network (LAN/Wi-Fi).**
- **Attacker sends a fake ARP reply** claiming, **"I am the router."**
- **Victim updates its ARP table** with the attacker's MAC address instead of the router's MAC.
- **Attacker also sends a fake ARP reply to the router** claiming, **"I am the victim."**
- **Router updates its ARP table** with the attacker's MAC address.
- **All traffic from the victim is now sent to the attacker.**
- **The attacker intercepts, monitors, or modifies the traffic.**
- **The attacker forwards the traffic to the real router**, so communication continues without the victim noticing.

#### SOC Indicators of ARP Spoofing

- Duplicate MAC addresses.
- ARP table changes.
- Sudden traffic rerouting.
- Internal network anomalies.
- Unexpected gateway MAC address.
- Excessive ARP replies.

## 2. DNS Spoofing

**DNS Spoofing (DNS Cache Poisoning)** is a cyberattack in which an attacker **provides false DNS information** so that a user is redirected from a legitimate website to a **fake or malicious website**.

DNS Spoofing is an attack where fake DNS records are used to redirect users from a legitimate website to a malicious website.

```
User
  │
  ▼
DNS Query (www.bank.com)
  │
  ▼
Compromised DNS Server / Fake DNS Response
  │
  ▼
Attacker's Website
  │
  ▼
Credentials Stolen
```

#### How DNS Spoofing Works

- **User enters a website** (e.g., `www.bank.com`).
- **The computer sends a DNS query** to resolve the domain name.
- **The attacker poisons the DNS cache** or sends a fake DNS response.
- **The DNS server returns the attacker's IP address** instead of the legitimate IP.
- **The user's browser connects to the fake website.**
- **The user enters login credentials or sensitive information.**
- **The attacker captures the information** while the user believes they are on the real website.

#### SOC Indicators for DNS Spoofing

- Unexpected DNS record changes.
- DNS responses pointing to unknown or malicious IP addresses.
- DNS cache modifications.
- Multiple users redirected to the same suspicious IP.
- DNS requests to unusual or unauthorized DNS servers.
- SSL/TLS certificate warnings after DNS resolution.
- Sudden increase in failed DNS lookups or unusual DNS traffic.

## 3. SSL Stripping 

**SSL Stripping** is a **Man-in-the-Middle (MITM) attack** in which an attacker **downgrades a secure HTTPS connection to an insecure HTTP connection**, allowing them to intercept and read the victim's data.

SSL Stripping is a MITM attack where an attacker converts an HTTPS connection into HTTP, allowing them to intercept unencrypted communication.

#### How SSL Stripping Works

- The victim opens a website (e.g., http://example.com).
- The attacker positions themselves between the victim and the web server (MITM).
- The website attempts to redirect the victim from HTTP to HTTPS.
- The attacker intercepts and removes the HTTPS redirect.
- The victim continues communicating over HTTP (unencrypted).
- The attacker communicates with the real website using HTTPS (encrypted).
- The attacker reads, captures, or modifies the victim's unencrypted HTTP traffic.
- The attacker forwards the traffic to the legitimate server.
- The server responds to the attacker over HTTPS.
- The attacker sends the response back to the victim over HTTP, keeping the victim unaware of the attack.

#### SOC Indicators for SSL Stripping

- Unexpected **HTTP** traffic to websites that normally use **HTTPS**.
- Missing HTTPS redirects.
- Absence of TLS/SSL handshake for secure websites.
- Users receiving "Not Secure" browser warnings.
- Sensitive data transmitted over HTTP.
- Proxy or gateway logs showing HTTP requests to secure domains.

## 4. Session Hijacking

**Session Hijacking** is a cyberattack in which an attacker **steals or takes over a user's active session** by obtaining the **session ID (session cookie/token)**, allowing the attacker to impersonate the legitimate user without knowing the password.

Session Hijacking is an attack where an attacker steals a user's session ID or session cookie to gain unauthorized access to their active session.

- Bypass the login process.
- Access user accounts without a password.
- Steal sensitive information.
- Perform unauthorized actions as the victim.
- Take over authenticated sessions.

#### How Session Hijacking Works

- **The user logs in** to a website successfully.
- **The server creates a session ID (session cookie/token)** for the user.
- **The browser stores the session ID** and sends it with every request.
- **The attacker steals the session ID** (e.g., through XSS, MITM, malware, or insecure HTTP).
- **The attacker sends requests using the stolen session ID.**
- **The server accepts the session ID** and believes the attacker is the legitimate user.
- **The attacker gains access** to the victim's account without entering a password.

#### SOC Indicators for Session Hijacking

- Same session ID used from different IP addresses.
- Session used from different geographic locations.
- Sudden change in User-Agent or browser fingerprint.
- Simultaneous logins using the same session.
- Unusual account activity after login.
- Session reuse after logout or expiration.
- Unexpected privileged actions within an active session.

## 5. Evil Twin Attack

An Evil Twin Attack is a wireless network attack in which an attacker creates a **fake Wi-Fi access point** that looks identical to a legitimate Wi-Fi network to trick users into connecting. Once connected, the attacker can monitor traffic, steal sensitive information, or launch further attacks.

This often lead to:
- MITM
- Credential theft
- Cookie stealing
- Fake captive portal login pages

#### How an Evil Twin Attack Works

1. The attacker creates a fake Wi-Fi access point with the same name as a legitimate network.
2. The victim sees both Wi-Fi networks and connects to the fake one.
3. All internet traffic passes through the attacker's device.
4. The attacker monitors, captures, or modifies the traffic.
5. Sensitive information such as usernames, passwords, and banking details can be stolen.

#### SOC Detection of Evil Twin Attack

- Detect unauthorized or rogue access points.
- Monitor duplicate or similar SSIDs.
- ARP Spoofing alerts
- Unusual DHCP server detected
- Network traffic interception pattern

---

# Distributed Denial of Service (DDoS) Attack

**DDoS (Distributed Denial-of-Service)** is a cyberattack in which **multiple compromised devices (botnet)** send a massive amount of traffic to a target server, website, or network, making it **slow, unavailable, or completely inaccessible** to legitimate users.

`A Botnet is a group of malware-infected devices that are remotely controlled by an attacker to perform cyberattacks.`

The attacker can command all the infected devices to perform malicious activities simultaneously.

```

            Attacker
                │
                ▼
    Botnet (Thousands of Bots)
      ┌──────┬──────┬──────┐
      ▼      ▼      ▼      ▼
    Bot1    Bot2   Bot3   BotN
      \       |      |      /
       \      |      |     /
        ▼     ▼      ▼    ▼
          Target Server
                │
                ▼
      Service Unavailable
```

- Disrupt business operations.
- Make websites or services unavailable.
- Demand ransom (Ransom DDoS).
- Damage an organization's reputation.
- Distract security teams while another attack occurs.

#### How DDoS Attack Works

1. **The attacker infects many devices with malware.**
2. **The infected devices become part of a botnet.**
3. **The attacker sends a command to the botnet.**
4. **All bots simultaneously send huge amounts of traffic to the target server.**
5. **The server's bandwidth, CPU, or memory becomes overloaded.**
6. **Legitimate users cannot access the service.**
7. **The website or application becomes slow or unavailable.**

#### SOC Indicators of DDoS

- Sudden spike in network traffic.
- Large number of requests from multiple IP addresses.
- High bandwidth utilization.
- Increased CPU and memory usage on servers.
- Numerous half-open TCP connections (SYN Flood).
- High rate of HTTP requests.
- Increased packet drops or network latency.
- Website or application becomes slow or unavailable.
- Firewall or IDS/IPS generates DDoS alerts.

### Types of DDoS Attacks

### 1. Volumetric Attack

A **Volumetric Attack** floods the target with an extremely large amount of traffic to **consume the available network bandwidth**, making the website or server unreachable.

**Target**

- Network bandwidth

**Example:** 

- UDP Flood
- ICMP (Ping) Flood
- DNS Amplification Attack

##### How It Works

1. The attacker controls a botnet.
2. The botnet sends millions of packets to the target.
3. The network bandwidth becomes fully utilized.
4. Legitimate traffic cannot reach the server.
5. The website or service becomes unavailable.

## 2. Protocol Attack

A **Protocol Attack** exploits weaknesses in network protocols (such as TCP/IP) to consume server or firewall resources instead of bandwidth.

**Target**

- Server resources (CPU, memory, connection table, firewall)

**Example:**

- SYN Flood
- ACK Flood
- Ping of Death
- Smurf Attack

##### How It Works (Single Points)

1. The attacker sends specially crafted protocol requests.
2. The server allocates resources for each request.
3. The attacker never completes the connection.
4. The server's connection table or resources become exhausted.
5. Legitimate users cannot establish new connections.

## Application Layer Attack

An Application Layer Attack overwhelms a web application by sending **excessive HTTP requests.**

**Target**

- Web server and application resources

**Example:**

- HTTP GET Flood
- HTTP POST Flood
- Slowloris Attack
##### How It Works (Single Points)

1. The attacker sends thousands of HTTP requests.
2. The web server processes each request.
3. CPU and memory usage increase.
4. The application becomes slow or unresponsive.
5. Legitimate users cannot access the website.


|Attack Type|Target|Goal|Common Examples|
|---|---|---|---|
|**Volumetric Attack**|Network bandwidth|Consume bandwidth|UDP Flood, ICMP Flood, DNS Amplification|
|**Protocol Attack**|Network protocols and server resources|Exhaust connection tables, CPU, or memory|SYN Flood, ACK Flood, Ping of Death|
|**Application Layer Attack**|Web application (Layer 7)|Overwhelm the application|HTTP GET Flood, HTTP POST Flood, Slowloris|

---
# DDoS Mitigation

- Rate Limiting
- Web Application firewall
- CDN (Cloudflare, Akamai)
- Traffic Filtering
- Load Balancing
- IP Blocking

---
# MITM vs DDoS

|**Feature**|**MITM (Man-in-the-Middle)**|**DDoS (Distributed Denial-of-Service)**|
|---|---|---|
|**Purpose**|Intercept or modify communication between two parties.|Make a service unavailable by overwhelming it with traffic.|
|**Goal**|Steal data, credentials, or monitor communication.|Disrupt or shut down a website, server, or network.|
|**Attack Method**|Attacker places themselves between the victim and the server.|Multiple compromised devices (botnet) flood the target with traffic.|
|**Target**|User communication and sensitive data.|Server, network, or application resources.|
|**Uses Botnet?**|No (not required).|Yes, typically uses a botnet.|
|**Data Theft**|Yes.|No (primary goal is disruption, not theft).|
|**Affects Availability?**|Usually No.|Yes.|
|**Affects Confidentiality?**|Yes.|No.|
|**Common Techniques**|ARP Spoofing, DNS Spoofing, SSL Stripping, Session Hijacking.|Volumetric Attacks, SYN Flood, HTTP Flood, UDP Flood.|
|**CIA Triad Impact**|**Confidentiality** (and sometimes Integrity).|**Availability**.|

