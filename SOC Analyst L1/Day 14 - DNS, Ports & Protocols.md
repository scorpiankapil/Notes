# Protocols

Web protocols are communication rules that allow browsers and servers to exchange data over the internet.

|Protocol|Full Form|Purpose|Default Port|
|---|---|---|--:|
|**HTTP**|HyperText Transfer Protocol|Transfers web pages (not secure)|**80**|
|**HTTPS**|HyperText Transfer Protocol Secure|Securely transfers web pages using SSL/TLS|**443**|
|**FTP**|File Transfer Protocol|Transfers files|**21**|
|**SFTP**|SSH File Transfer Protocol|Secure file transfer|**22**|
|**SMTP**|Simple Mail Transfer Protocol|Sends emails|**25**, **587**, **465**|
|**POP3**|Post Office Protocol v3|Receives/downloads emails|**110**, **995**|
|**IMAP**|Internet Message Access Protocol|Accesses and syncs emails|**143**, **993**|
|**DNS**|Domain Name System|Converts domain names to IP addresses|**53**|
|**SSH**|Secure Shell|Secure remote login|**22**|

**Without protocols, devices wouldn't understand each other**

## Where Do Web Protocols Fit?

|**OSI Layer**|**Protocols**|**Purpose**|
|---|---|---|
|**Application Layer**|HTTP, HTTPS, DNS, FTP|Provides web services, web browsing, domain name resolution, and file transfer.|
|**Transport Layer**|TCP, UDP|Ensures data is delivered using port numbers and manages communication between applications.|
|**Network Layer**|IP|Routes packets from the source to the destination using IP addresses.|
|**Data Link Layer**|Ethernet, Wi-Fi|Transfers data between devices on the same local network using MAC addresses.|

---
### HTTP

**HTTP (HyperText Transfer Protocol)** is a protocol used to transfer web pages and data between a **web browser (client)** and a **web server**.

It **does not encrypt** the data, so anyone intercepting the traffic may be able to read it.

- Default Port: **80**
- Data is **not encrypted**.
- Faster than HTTPS because no encryption is performed.
- Used for websites where security is not required.

### HTTPS

**HTTPS (HyperText Transfer Protocol Secure)** is the secure version of HTTP. It uses **SSL/TLS encryption** to protect data exchanged between the browser and the web server.

- Default Port: **443**
- Data is **encrypted**.
- Protects passwords, banking details, and personal information.
- Prevents eavesdropping and data tampering.

##### SSL (Secure Socket Layer)

**SSL (Secure Sockets Layer)** is a security protocol developed to **encrypt communication** between a client (browser) and a server.

Today, **SSL is not in use anymore** because it has known security vulnerabilities and has been replaced by **TLS**.

- Encrypts data during transmission.
- Provides confidentiality and authentication.
- Used by HTTPS.
- **Deprecated** (no longer recommended).

##### TLS (Transport Layer Security)

**TLS (Transport Layer Security)** is the **modern and more secure version of SSL**. It encrypts communication between clients and servers, ensuring that data remains confidential and cannot be easily intercepted or modified.

- Successor to SSL.
- Provides encryption, authentication, and data integrity.
- Used by HTTPS, email, VPNs, and many other secure services.
- Currently the industry standard.

#### HTTP Methods

**HTTP methods** are actions that tell the web server **what operation the client wants to perform** on a resource.

|Method|Purpose|Example|
|---|---|---|
|**GET**|Retrieve data from the server.|View a webpage or user profile.|
|**POST**|Send new data to the server.|Submit a login form or create a new account.|
|**PUT**|Update or replace an existing resource.|Update a user's profile.|
|**PATCH**|Partially update an existing resource.|Change only the user's email address.|
|**DELETE**|Remove a resource from the server.|Delete a user account.|
|**HEAD**|Retrieve only the response headers, not the body.|Check if a file exists.|
|**OPTIONS**|Show which HTTP methods are supported by the server.|Check API capabilities (used in CORS).|

#### HTTP Status codes

HTTP status codes are server responses that indicate whether an HTTP request was successful, redirected, resulted in a client error, or failed due to a server error.

**Responses are grouped in five classes:** 

1. Informational Responses (100-199)
2. Successful Responses (200-299)
3. Redirection Messages (300-399)
4. Client Error Response (400-499)
5. Server Error Response (500-599)

| **Status Code** | **Why It Matters**                                                              |
| --------------: | ------------------------------------------------------------------------------- |
|         **200** | Normal successful requests.                                                     |
|   **301 / 302** | Redirects; investigate suspicious redirects or phishing.                        |
|         **304** | Browser cache usage.                                                            |
|         **400** | Malformed requests; may indicate scanning or fuzzing.                           |
|         **401** | Failed authentication; monitor for brute-force attacks.                         |
|         **403** | Unauthorized access attempts.                                                   |
|         **404** | Resource not found; common during reconnaissance or directory scanning.         |
|         **405** | Unsupported method; may indicate probing of APIs.                               |
|         **408** | Client timeout; possible network issues or slow attacks.                        |
|         **409** | Resource conflict.                                                              |
|         **413** | Oversized payloads; possible abuse or upload attacks.                           |
|         **429** | Rate limiting triggered; often indicates brute-force or automated requests.     |
|         **500** | Internal server errors; may indicate application bugs or exploitation attempts. |
|         **502** | Upstream server/proxy issues.                                                   |
|         **503** | Service unavailable; possible maintenance or DDoS attack.                       |
|         **504** | Backend server timeout; overloaded or unavailable services.                     |

---
### Domain Name System (DNS)

DNS is a naming system that translates a domain name into an IP address so your computer can find the correct server on the Internet.

```
google.com
facebook.com
chat.openai.com

```

```
142.250.183.14
31.13.71.36
104.18.x.x
```

#### Working of DNS

1. The user enters a website name, such as **[www.google.com](http://www.google.com)**, in the browser.
2. The computer checks its **local DNS cache** to see if the IP address is already stored.
3. If the IP address is not found, the computer sends a **DNS query** to its DNS server.
4. The DNS server checks its own cache for the requested domain.
5. If the DNS server does not have the record, it contacts a **Root DNS Server**.
6. The Root DNS Server directs the DNS server to the appropriate **Top-Level Domain (TLD) Server** (e.g., `.com`).
7. The TLD server provides the address of the **authoritative DNS server** for the domain (e.g., `google.com`).
8. The DNS server contacts the authoritative DNS server and requests the IP address of the website.
9. The authoritative DNS server returns the IP address, and the DNS server stores it in its cache.
10. The DNS server sends the IP address to the client, and the browser uses it to connect to the website and display the webpage

```
User Types Website Name  
        ↓  
Check Local DNS Cache  
        ↓  
DNS Server  
        ↓  
Root DNS Server  
        ↓  
TLD Server (.com, .org, .net)  
        ↓  
Authoritative DNS Server  
        ↓  
IP Address Found  
        ↓  
DNS Server Caches Result  
        ↓  
IP Address Returned  
        ↓  
Browser Connects to Website
```

#### SOC Indicators

- Too many DNS requests
- Suspicious domains
- Random subdomains
- DNS Tunneling

#### Attacks

- DNS Spoofing 
- DNS Tunneling (data exfiltration)
- DGA (Domain Generation Algorithm)

---
### FTP (File Transfer Protocol)

**FTP (File Transfer Protocol)** is a standard network protocol used to **transfer files** between a client and a server over a network.

- Used for file transfer.
- **Does not encrypt** data.
- Username, password, and files are sent in **plain text**.
- Less secure.

**Default Ports**

- **Port 21** → Control connection
- **Port 20** → Data transfer (Active Mode)

### SFTP (SSH File Transfer Protocol)

**SFTP (SSH File Transfer Protocol)** is a secure file transfer protocol that runs over **SSH (Secure Shell)** and encrypts all communication between a client and a server over a network.

- Uses SSH for security.
- Encrypts usernames, passwords, and files.
- Provides authentication, confidentiality, and integrity.
- More secure than FTP.

**Default Port**

- **Port 22**

#### SOC Indicators

- Large file transfer
- Unknown uploads
- Anonymous login

#### Attacks

- Credential sniffing (FTP)
- Data exfiltration
- Brute force login

---

### SMTP (Simple Mail Transfer Protocol)

**SMTP (Simple Mail Transfer Protocol)** is a protocol used to **send emails** over the Internet. It transfers emails from the sender's email client to the recipient's mail server.

- Sending emails.
- Relaying emails between mail servers.
- Delivering outgoing emails.

**Note:** SMTP is only used for **sending** emails. To **receive** emails, protocols like **POP3** or **IMAP** are used.

**Default Ports**

- **Port 25** - SMTP
- **Port 587** - Secure Submission

| Port    | Encryption | Use                                                    |
| ------- | ---------- | ------------------------------------------------------ |
| **25**  | No         | Mail server to mail server communication (SMTP relay). |
| **587** | STARTTLS   | Email submission from clients (recommended).           |
| **465** | SSL/TLS    | Secure SMTP (SMTPS).                                   |

#### SOC Indicators

- Bulk email sending
- Unknown sender domains
- Email spoofing

#### Attacks

- Phishing 
- Spam campaigns
- Email spoofing

---

### SSH (Secure Shell)

**SSH (Secure Shell)** is a **secure network protocol** used to remotely access and manage computers or servers over an encrypted connection.

- Secure remote login.
- Executing commands on remote systems.
- Secure file transfer (SFTP/SCP).
- Server administration.
- Secure tunneling and port forwarding.

**Default Port**

- **Port 22**

##### Authentication Methods

| Method                        | Description                                                   |
| ----------------------------- | ------------------------------------------------------------- |
| **Password Authentication**   | User logs in with a username and password.                    |
| **Public Key Authentication** | User logs in using an SSH key pair (public and private keys). |

#### SOC Indicators

- Multiple failed logins
- Login from unusual  IP
- Root login attempts

#### Attacks

- Brute force
- Credential theft
- Unauthorized access

--- 

### RDP (Remote Desktop Protocol)

**RDP (Remote Desktop Protocol)** is a proprietary protocol developed by **Microsoft** that allows a user to **remotely access and control another computer** over a network using a graphical interface.

- Remote desktop access.
- Managing Windows servers.
- Technical support.
- Remote work.
- Accessing office computers from home.

**Default Port**

- **Port 3389**

#### SOC Indicators

- Login at odd hours
- Multiple login attempts
- External IP login

#### Attacks

- RDP brute force
- Lateral movement
- Ransomware entry point

---

### SMB (Server Message Block)

**SMB (Server Message Block)** is a network protocol used to **share files, folders, printers, and other resources** between computers on a network.

It is primarily used in **Windows** environments but is also supported by Linux (via Samba) and macOS.

- File sharing.
- Folder sharing.
- Printer sharing.
- Network drive access.
- Sharing resources between computers.

**Default Ports**

|Protocol|Port|Purpose|
|---|---|---|
|**SMB**|**TCP 445**|Modern SMB communication (SMBv2/SMBv3).|
|**NetBIOS SMB**|**TCP 139**|Older SMB communication using NetBIOS.|

#### SOC Indicators

- Access to admin shares (C$)
- File movement across systems
- Lateral movement
#### Attacks

- EternalBlue exploit
- SMB relay
- Lateral movement

---

# Computer Ports

A **computer port** is a **logical communication endpoint** that allows applications and services to send and receive data over a network.

A computer port is a numbered communication endpoint that identifies a specific service or application on a computer.

**Port identifies the specific application or service** running on that computer.

- There are 65,535 possible port numbers, although not all are in common use.
- Every **TCP/UDP port** has a unique number from **0 to 65535**.
- Ports identify **which application or service** should receive network data.
- **1. Well-Known Ports (0–1023)**
    - These ports are **reserved for common, standard Internet services**. They are assigned by **IANA (Internet Assigned Numbers Authority)**.

|Port|Protocol|Service|
|---|---|---|
|20/21|FTP|File Transfer|
|22|SSH|Secure Remote Login|
|23|Telnet|Remote Login (Insecure)|
|25|SMTP|Email Sending|
|53|DNS|Domain Name Resolution|
|80|HTTP|Web Browsing|
|110|POP3|Receive Email|
|143|IMAP|Email Synchronization|
|443|HTTPS|Secure Web Browsing|

- **2. Registered Ports (1024–49151)**
    - These ports are assigned to **specific applications and services**. They are commonly used by software vendors.

|Port|Application|
|---|---|
|1433|Microsoft SQL Server|
|1521|Oracle Database|
|3306|MySQL|
|3389|Remote Desktop (RDP)|
|5432|PostgreSQL|
|5900|VNC|


- **3. Dynamic / Private (Ephemeral) Ports (49152–65535)**
    - These are **temporary ports** automatically assigned by the operating system to the **client** when it initiates a connection.

```
Your PC
192.168.1.10:52045
        │
        ▼
Google Server
142.250.x.x:443
```

