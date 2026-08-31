# Router

A Router is a networking device used to connect different networks and forward data packets between them using IP addresses.

```
LAN --> Router --> Internet
```

It works at the Network Layer (Layer 3) of the OSI model.

- Connects multiple networks
- Routes data packets to the correct destination
- Uses IP addresses for communication
- Chooses the best path for data transmission
- Allows communication between different VLANs/networks
- Connects LAN to the WAN and Internet.

### Working of Router

1. The router receives a data packet.
2. It checks the destination IP address.
3. The router compares the address with its routing table.
4. It selects the best path.
5. The packet is forwarded to the next network or destination.


### SOC Logs from Router

- Source IP
- Destination IP
- Traffic flow

### SOC Indicators

- Traffic to malicious IP
- Unusual outbound connections
- Data exfiltration

# Switches

A switch is a network device used to connect multiple devices inside a network. It is also called Switching Hub.

It works at the Data Link Layer (Layer 2) of OSI Model and it use MAC Addresses to send data to required devices.

A switch works smarter than a hub because it sends data only to the required device instead of all devices.

```
PC --> Switch --> Server
```

- Connects multiple devices in a LAN
- Forwards data to the correct destination device
- Uses MAC addresses for communication
- Reduces network traffic
- Minimizes data collisions

### Working of Switches

- A device sends a data frame to the switch.
- The switch receives the frame on one of its ports.
- It reads the source MAC address and stores it in its MAC address table.
- The switch checks the destination MAC address in the frame.
- If the destination MAC address exists in the MAC table, the switch forwards the data only to the correct port.
- If the destination MAC address is unknown, the switch broadcasts the frame to all ports except the sender’s port.
- The destination device receives the data and communication takes place successfully.


### SOC Perspective

- Detect internal movement
- MAC anomalies

### Threat

- ARP Spoofing
- MAC flooding

# VPN (Virtual Private Network)

A Virtual Private Network (VPN) is a security technology that **creates an encrypted tunnel between your device and a VPN server over the internet**, so your traffic travels privately and your real IP address is hidden.

```
User --> Encrypted Tunnel --> VPN Server --> Internet
```

- Encrypts your internet traffic (Confidentiality)
- Hides your real IP address (Anonymity)
- Helps access content that may be restricted by location.
- Allow remote access

## Types of VPN

### 1.Remote Access VPN (Client-to-Site VPN)

A **Remote Access VPN** allows an individual user to securely connect to a private network from a remote location over the Internet.

- Employee working from home.
- Student accessing a college network remotely.

```
Remote Access VPN

Laptop
   │
Encrypted Tunnel
   │
VPN Server
   │
Company Network
```

### 2. Site-to-Site VPN

A **Site-to-Site VPN** securely connects two or more different networks over the Internet.

- Connecting a company's Head Office to Branch Offices.
- Secure communication between two company locations.

```
Site-to-Site VPN

Office A Network
       │
   VPN Gateway
       │
Encrypted Tunnel
       │
   VPN Gateway
       │
Office B Network
```


### 3. SSL VPN

**SSL VPN (Secure Sockets Layer Virtual Private Network)** is a type of VPN that uses **SSL/TLS encryption** to create a secure connection between a user's device and a private network over the Internet.

- Uses in HTTPS (Port 443)
- Common in corporate setup

```
Employee Laptop
        │
  SSL/TLS Encrypted Tunnel
        │
        ▼
   SSL VPN Gateway
        │
        ▼
 Company Network
        │
        ▼
 File Server / Applications
```

## How VPN Bypasses a Blocked Website?

- You connect your device to a **VPN server**.
- The VPN creates a **secure, encrypted tunnel** between your device and the VPN server.
- All your internet traffic is **encrypted** before leaving your device.
- The college firewall receives only **encrypted VPN traffic**.
- The firewall can see that you are connected to a **VPN server**, but it **cannot see the websites** you are visiting through the tunnel (unless it uses advanced inspection or blocks the VPN itself).
- The firewall allows the connection if VPN traffic is not blocked.
- The VPN server decrypts your request.
- The VPN server accesses the blocked website on your behalf.
- The website sends the response back to the VPN server.
- The VPN server encrypts the response and sends it back to your device.
- Your VPN decrypts the response, and the website loads normally.

```
Laptop
   │
Encrypted VPN Tunnel
   │
College Firewall (Sees only VPN)
   │
VPN Server
   │
Blocked Website
   │
VPN Server
   │
Encrypted VPN Tunnel
   │
Laptop
```

### Suspicious Indicators

1. Login from an unusual country.
2. Multiple logins for the same user from different locations.
3. VPN login followed by suspicious activity.
4. Unusually high data transfer through a VPN.

### Common VPN Abuse (Single Points)

**Attackers use VPNs to:** 
- Hide identity
- Bypass geo locations
- Access internal network

### SOC Example

- User: Admin
- Login IP: Germany
- VPN IP: India
- Time gap: 2 minutes

- Impossible travel --> Compromised Account

# Firewall

A firewall is a network security device or software that monitors, filters, and controls incoming and outgoing network traffic based on predefined security rules.

A firewall:

- Allows safe/authorized traffic
- Blocks harmful or unauthorized traffic

The firewall administrator decides:

- What traffic is allowed
- What traffic is blocked

### Working of Firewall

- A device sends or receives network traffic (data packets).
- The firewall intercepts and examines the incoming or outgoing traffic.
- It checks the traffic against predefined security rules and policies.
- Legitimate and trusted traffic is allowed to pass through.
- Suspicious, unauthorized, or malicious traffic is blocked or denied.


## Inbound Rules & Outbound Rules

| **Inbound Rules**                               | **Outbound Rules**                                     |
| ----------------------------------------------- | ------------------------------------------------------ |
| Control incoming traffic                        | Control outgoing traffic                               |
| Protect system from external threats            | Control what leaves the system                         |
| Applied to traffic entering the network/device  | Applied to traffic leaving the network/device          |
| Blocks unauthorized access attempts             | Prevents unauthorized external connections             |
| Example: Block hackers trying to access your PC | Example: Block malware from connecting to the internet |
- **Inbound Rules** → What can enter your system
- **Outbound Rules** → What can leave your system

# Intrusion Detection System (IDS)

An Intrusion Detection System (IDS) is a security tool that monitors network traffic or system activities to detect suspicious behavior, unauthorized access, or cyber attacks.

It alerts security teams when malicious activity is detected.

IDS works together with Firewalls, Antivirus and Other security devices

- Monitor network traffic
- Detect cyber attacks
- Identify suspicious activities
- Generate security alerts
- Help SOC teams investigate threats

### Working of IDS

- IDS continuously monitors network traffic or system activities.
- It analyzes the traffic and behavior for suspicious patterns.
- IDS compares activities with known attack signatures or abnormal behavior.
- If suspicious activity is detected, IDS generates an alert.
- Security teams or SOC analysts investigate and respond to the threat.

## IDS can be Passive or Active

| **Active IDS**                           | **Passive IDS**                              |
| ---------------------------------------- | -------------------------------------------- |
| Detects and takes action against attacks | Detects attacks but does not take action     |
| Monitors and blocks suspicious activity  | Only monitors and logs suspicious activity   |
| Can disconnect or block attacker         | Only sends alerts/notifications              |
| Provides automatic response              | Requires administrator action                |
| More secure and protective               | Mainly used for monitoring and investigation |
| Example: Blocks system doing port scan   | Example: Logs port scan activity only        |

# Intrusion Prevention System (IPS)

An **Intrusion Prevention System (IPS)** is a security tool that monitors network traffic or system activities to detect and **automatically block** suspicious behavior, unauthorized access, or cyber attacks in real time.

Unlike an IDS, an IPS not only detects threats but also **takes immediate action** to stop them.

IPS works together with **Firewalls, IDS, Antivirus, and other security devices**.

- Monitor network traffic
- Detect cyber attacks
- Identify suspicious activities
- Automatically block malicious traffic
- Prevent unauthorized access
- Generate security alerts
- Help SOC teams investigate threats

### Working of IPS

- IPS continuously monitors network traffic or system activities.
- It analyzes the traffic and behavior for suspicious patterns.
- IPS compares activities with known attack signatures or abnormal behavior.
- If suspicious activity is detected, IPS automatically blocks or drops the malicious traffic.
- IPS generates an alert and logs the event.
- Security teams or SOC analysts review the alerts and investigate the incident.

# IDS vs IPS

| **IDS (Intrusion Detection System)** | **IPS (Intrusion Prevention System)** |
| ------------------------------------ | ------------------------------------- |
| Detects attacks                      | Detects **and blocks** attacks        |
| Generates alerts                     | Generates alerts and takes action     |
| Passive security device              | Active security device                |
| Does not stop malicious traffic      | Automatically stops malicious traffic |
| Helps analysts investigate           | Prevents attacks in real time         |

- **IDS = Detect & Alert** 👀
- **IPS = Detect, Alert & Block** 🛡️

---
# Proxy Servers

A Proxy server is a system that acts as a middle layer between your a client (user) and a destination server you visit. Instead of directly connecting to a server, your request goes through a proxy server, which communicates with the server on behalf of client. 

In simple words, destination server sees proxy server not client

It does not encrypt data like VPN.

- Acts as a **middleman** between the client and the server.
- Hides the client's **IP address**.
- Forwards requests and responses.
- Can filter or block websites.
- Can cache web content to improve speed.
- **Usually does not encrypt** network traffic.
- Bypassing geo-restrictions

|**VPN**|**Proxy Server**|
|---|---|
|Encrypts all internet traffic|Usually does **not** encrypt traffic|
|Hides your IP address|Hides your IP address|
|Protects the **entire device**|Usually works for a **specific application** (e.g., browser)|
|Provides privacy and security|Mainly used for access control, filtering, or hiding IP|
|Creates an **encrypted tunnel**|Simply forwards your requests|
|Slower due to encryption|Usually faster because little or no encryption is used|

### Forward Proxy vs Reverse Proxy

#### Forward Proxy

A **Forward Proxy** sits **between the client (user) and the internet**. It receives requests from the user, forwards them to the destination server, and returns the response.

##### How It Works 

1. User sends a request to access a website.
2. The request goes to the **Forward Proxy**.
3. The proxy checks its security or access rules.
4. If allowed, it forwards the request to the website.
5. The website sends the response back to the proxy.
6. The proxy returns the response to the user.
7. The website sees the **Proxy Server's IP address**, not the user's IP.

#### Reverse Proxy

A **Reverse Proxy** sits **in front of one or more web servers**. It receives requests from users and forwards them to the appropriate backend server.

##### How It Works 

1. A user sends a request to a website.
2. The request reaches the **Reverse Proxy**.
3. The Reverse Proxy checks security rules.
4. It forwards the request to the appropriate backend server.
5. The server processes the request.
6. The response is sent back to the Reverse Proxy.
7. The Reverse Proxy returns the response to the user.
8. The user sees only the **Reverse Proxy**, not the actual backend server.

| **Forward Proxy**                      | **Reverse Proxy**                      |
| -------------------------------------- | -------------------------------------- |
| Works on behalf of the **client**      | Works on behalf of the **server**      |
| Sits between the user and the internet | Sits between users and web servers     |
| Hides the client's IP address          | Hides the server's IP address          |
| Used to control users' internet access | Used to protect and manage web servers |
| Common in schools and organizations    | Common in data centers and websites    |

```
 FORWARD PROXY                                      REVERSE PROXY         

User (Client)                                      User (Client)
      │                                                  │
      ▼                                                  ▼
+----------------+                               +----------------+
| Forward Proxy  |                               | Reverse Proxy  |
+----------------+                               +----------------+
      │                                                  │
      ▼                                         ├──────► Web Server 1
Internet / Website                              ├──────► Web Server 2
                                                └──────► Web Server 3

Acts on behalf of the Client               Acts on behalf of the Server

  Hides Client IP                                 Hides Server IP
```

