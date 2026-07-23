# OSI Model

The OSI (Open Systems Interconnection) Model was created by International Organization for Standardization(ISO) in 1984 to define standard rules for network communication between different devices and networking products.

The OSI model has:

- 7 layers

Each layer performs a specific task during communication.

## Purpose of OSI Model

The OSI model helps:

- Different devices communicate properly
- Standardize networking
- Troubleshoot network problems easily

# 7 Layers of OSI Model

From top to bottom:

|Layer Number|OSI Layer (Sender Side)|Data Flow|
|---|---|---|
|7|Application Layer|↓|
|6|Presentation Layer|↓|
|5|Session Layer|↓|
|4|Transport Layer|↓|
|3|Network Layer|↓|
|2|Data Link Layer|↓|
|1|Physical Layer|↓|

| Layer Number | OSI Layer (Receiver Side) | Data Flow |
| ------------ | ------------------------- | --------- |
| 1            | Physical Layer            | ↑         |
| 2            | Data Link Layer           | ↑         |
| 3            | Network Layer             | ↑         |
| 4            | Transport Layer           | ↑         |
| 5            | Session Layer             | ↑         |
| 6            | Presentation Layer        | ↑         |
| 7            | Application Layer         | ↑         |
## Working of OSI Model

When data is sent from one computer to another:

1. Data starts from the Application Layer on the sending computer.
2. Data moves down through all 7 layers until it reaches the Physical Layer.
3. Data travels through the network medium (cable/wireless).
4. On the receiving computer, data starts from the Physical Layer.
5. Data moves back up through all layers until it reaches the Application Layer.

## Layer Communication

Each OSI layer communicates only with:

- The layer above it
- The layer below it

Example:

- Presentation Layer receives data from Application Layer
- Then sends it to Session Layer

It does not communicate directly with:

- Network Layer
- Data Link Layer

#### Important Concept

Whatever function is performed on the sending computer is reversed on the receiving computer at the same layer.

Example:

- If Presentation Layer compresses data on sender side
- Presentation Layer decompresses data on receiver side

##### Example

Suppose:

- COMPUTER1 sends data to SERVER1

The data:

1. Moves down all OSI layers on COMPUTER1
2. Travels across the network
3. Moves up all OSI layers on SERVER1

Then SERVER1 processes the original data.

---
# Layer 7: Application Layer

The Application Layer is the top layer of the OSI model and is responsible for providing network services directly to user applications.

This layer handles the actual network request made by the user.

Examples of requests:

- Opening a website
- Sending an e-mail
- Accessing shared files

The Application Layer communicates with software such as:

- Web browsers
- E-mail applications
- File-sharing programs

##### Functions of Application Layer

- Provides network services to applications
- Creates user requests
- Allows communication between applications and network

##### Common Protocols

- HTTP → Web browsing
- HTTPS → Secure web browsing
- SMTP → Sending e-mails
- FTP → File transfer
- DNS → Name resolution

##### Example

Suppose:

- You type `www.google.com` in a web browser on COMPUTER1.

The Application Layer:

1. Creates an HTTP request
2. Sends the request to lower OSI layers
3. Data travels across the network
4. On SERVER1, the Application Layer passes the request to the web server application

### SOC Perspective

- Phishing attacks
- Malicious URLs
- Suspicious API calls

# Layer 6: Presentation Layer

The Presentation Layer is the 6th layer of the OSI model and is responsible for formatting, translating, encrypting, and compressing data before transmission.

It acts as a translator between the Application Layer and lower OSI layers.

The Presentation Layer ensures that data sent from one system can be understood correctly by the receiving system.

## Functions of Presentation Layer

#### Compression and Decompression

The Presentation Layer can compress data before transmission to reduce data size and improve speed.

On the receiving side:

- The Presentation Layer decompresses the data before passing it to the Application Layer.

#### Encryption and Decryption

The Presentation Layer can encrypt data for security before sending it across the network.

On the receiving side:

- It decrypts the data so the receiver can read it.

#### Character Code Translation

**Character Code Translation** is a function that converts data from one character encoding format to another so that different computer systems can correctly understand and display the data.

**Working of Code Translation:**

- The sender types a message (e.g., **HELLO**).
- The sender's computer encodes the message using its own character code (such as **ASCII**).
- The data reaches the **Presentation Layer**.
- The Presentation Layer checks the character encoding used by the sender.
- It determines the character encoding required by the receiving computer.
- If both systems use different character codes (e.g., **ASCII** and **EBCDIC**), the Presentation Layer converts the characters into the receiver's encoding.
- The translated data is sent over the network.
- The receiving computer receives the translated character codes.
- The receiver decodes the character codes and displays the original message correctly.

### SOC Perspective 

- Encryption analysis
- SSL stripping (MITM)

# Layer 5: Session Layer

The Session Layer is the 5th layer of the OSI model and is responsible for establishing, managing, and terminating communication sessions between two systems.

It controls the conversation (dialog) between devices during communication.

## Functions of Session Layer

#### 1. Session Establishment

Creates a session between sender and receiver before communication starts.

#### 2. Session Management

Controls and maintains communication between systems.

It defines rules such as:

- Who sends data
- When data is sent
- How much data is sent

#### 3. Session Termination

Closes the communication session properly after data transfer is complete.

##### Example

Suppose:

- COMPUTER1 wants to communicate with SERVER1.

The Session Layer:

1. Establishes a session
2. Manages communication during data transfer
3. Ends the session after communication finishes

### SOC Perspective

- Session Hijacking
- Session Cookies

# Layer 4: Transport Layer

The Transport Layer is the 4th layer of the OSI model. It is responsible for providing reliable communication and end-to-end data delivery between devices.

This layer takes data from the upper layers, breaks it into smaller units called segments, and ensures that the data reaches the destination correctly and in the proper order.

**Protocols:** 

- TCP (reliable)
- UDP (fast, unreliable)
## Functions of Transport Layer

#### 1. Segmentation

The Transport Layer breaks large data into smaller pieces called:

- Segments or packets

This makes transmission easier and faster.
#### 2. Reliable Delivery

For reliable communication, the Transport Layer:

- Checks whether packets reach destination
- Uses acknowledgments (ACKs)
- Retransmits missing packets if needed

#### 3. Reassembly

On the receiving side, the Transport Layer:

- Reassembles packets
- Reconstructs the original message

#### 4. Sequencing

Packets may arrive out of order on the network.

The Transport Layer uses sequence numbers to arrange packets in the correct order.

##### Example

Received order:

- 3, 1, 4, 2, 5

Transport Layer rearranges them into:

- 1, 2, 3, 4, 5

#### 5. Port Addressing

The Transport Layer uses:

- Port numbers (service addresses)

Ports identify which application should receive the data.

Examples:

- HTTP → Port 80
- HTTPS → Port 443
- FTP → Port 21

##### Example

Suppose:

- COMPUTER1 sends a web request to SERVER1.

The Transport Layer:

1. Breaks data into packets
2. Adds source and destination port numbers
3. Sends packets to lower layers
4. Receiver checks packets and rearranges them correctly

### SOC Perspective

- Port Scanning
- SYN Flood attacks
- Suspicious ports

# Layer 3: Network Layer

The Network Layer is the 3rd layer of the OSI model and is responsible for:

- Logical addressing
- Routing packets between networks

It ensures that data packets reach the correct destination network.

The network layer is responsible for determine the best path to send data across multiple network.

## Functions of Network Layer

#### 1. Logical Addressing

The Network Layer uses logical addresses to identify systems on a network.

In TCP/IP, the logical address is:

- IP address

Example:

- 192.168.1.10

Logical addresses identify:

- The host/device
- The network where the device exists

#### 2. Routing

The Network Layer routes packets from source to destination using routers.

Routers use:

- Routing tables

to find the best path for packet delivery.

#### 3. Packet Delivery

The Network Layer forwards packets between different networks until they reach the destination system.

## Logical Address vs MAC Address

#### Logical Address (IP Address)

- Assigned by software
- Can change
- Identifies network and host
- Used for routing across networks

#### MAC Address

- Physical address burned into NIC
- Permanent
- Identifies only the device
- Not used for routing between networks

##### Example

Suppose:

- COMPUTER1 sends a request to SERVER1.

The Network Layer:

1. Adds source IP address
2. Adds destination IP address
3. Routers read destination IP
4. Packet is forwarded through networks
5. Packet reaches SERVER1

### SOC Perspective

- IP tracking
- Geolocation
- Suspicious external connections

# Layer 2: Data Link Layer

The Data Link Layer is the 2nd layer of the OSI model and is responsible for:

- Physical addressing
- Error detection
- Converting packets into signals for transmission

It prepares data for communication on the local network.

## Functions of Data Link Layer

#### 1. Framing

The Data Link Layer converts packets received from the Network Layer into:

- Frames

#### 2. Physical Addressing

The Data Link Layer adds:

- Source MAC address
- Destination MAC address

MAC addresses identify devices on the local network.

#### 3. Error Detection and Control

The Data Link Layer checks for transmission errors and performs error correction/control functions.

#### 4. Media Access Control

It determines how devices place data on the network medium.

Examples:

- CSMA/CD
- Token Passing

## Sublayers of Data Link Layer

#### 1. LLC (Logical Link Control)

Responsible for:

- Error correction
- Flow control

#### 2. MAC (Media Access Control)

Responsible for:

- MAC addressing
- Access to network medium

##### MAC Address

A MAC address is the physical address burned into the network card (NIC).

Example:

- 00-90-4B-4C-C1-59

It is used to identify devices on the local network.

### Working of Data Link Layer

On the sending system:

1. Receives packets from Network Layer
2. Adds source and destination MAC addresses
3. Converts packets into binary/electrical signals
4. Sends signals to Physical Layer

On the receiving system:

1. Receives electrical signals from Physical Layer
2. Converts signals back into data/frames
3. Removes MAC information
4. Passes packets to Network Layer


# Layer 1: Physical Layer

The Physical Layer is the 1st and lowest layer of the OSI model. It is responsible for transmitting raw bits (0s and 1s) through the communication medium, such as cables, fiber optics, or wireless signals.

This layer deals with the physical and electrical parts of network communication.

## Functions of Physical Layer

#### 1. Bit Transmission

The Physical Layer sends and receives bits over the network medium.

#### 2. Physical Topology

Defines the physical layout/structure of the network.

Examples:

- Bus topology
- Star topology
- Ring topology

#### 3. Transmission Medium

Handles the physical media used for communication.

Examples:

- UTP cable
- Fiber-optic cable
- Coaxial cable
- Wireless signals

#### 4. Electrical and Signal Standards

Defines:

- Voltage levels
- Timing of signals
- Encoding of bits

### Working of Physical Layer

On the sending system:

1. Receives binary signals from Data Link Layer
2. Sends signals onto the communication medium

On the receiving system:

1. Receives signals from the medium
2. Passes signals to the Data Link Layer

##### Example

Suppose:

- COMPUTER1 sends data to SERVER1.

The Physical Layer:

- Transmits electrical/light signals through the cable or wireless medium
- SERVER1 receives those signals through its Physical Layer

#### Devices Working at Physical Layer

- Hubs
- Repeaters
- Cables
- Connectors


# **The OSI Model**

|Layer|Name|Easy Keyword to Remember|Main Things|
|---|---|---|---|
|7|Application|User Services|HTTP, FTP, SMTP, Browser|
|6|Presentation|Format & Security|Encryption, SSL/TLS, Compression|
|5|Session|Connection Control|Session, Dialog, Tunneling|
|4|Transport|Reliable Delivery|TCP, UDP, Segments, Ports|
|3|Network|Routing|IP Address, Router, Packet|
|2|Data Link|Local Delivery|MAC Address, Frame, Switch|
|1|Physical|Signals & Cables|Cables, Fiber, Electrical Signals|

| Layer | OSI Layer          | Common Protocols                                                 |
| ----- | ------------------ | ---------------------------------------------------------------- |
| 7     | Application Layer  | HTTP, HTTPS, FTP, SMTP, POP3, IMAP, DNS, DHCP, SNMP, Telnet, SSH |
| 6     | Presentation Layer | SSL, TLS, JPEG, MPEG, ASCII                                      |
| 5     | Session Layer      | NetBIOS, RPC, PPTP, SIP                                          |
| 4     | Transport Layer    | TCP, UDP, SPX                                                    |
| 3     | Network Layer      | IP, ICMP, IPX, ARP, RARP, OSPF, RIP                              |
| 2     | Data Link Layer    | Ethernet, PPP, HDLC, Frame Relay, ATM                            |
| 1     | Physical Layer     | UTP, Fiber Optic, Coaxial Cable, Bluetooth, Wi-Fi Signals        |


# How does communication happen in The OSI Model

## 1. Sender's Side (Encapsulation)

- The user creates data at the **Application Layer (Layer 7)**.
- The data moves **downward** through all 7 OSI layers.
- Each layer **adds its own header** (and the Data Link layer also adds a trailer/footer).
- This process of adding headers is called **Encapsulation**.

```
Application (Data Created)
        ↓
Presentation (Adds Header)
        ↓
Session (Adds Header)
        ↓
Transport (Adds Header)
        ↓
Network (Adds Header)
        ↓
Data Link (Adds Header + Trailer)
        ↓
Physical (Converts to Bits)
```

## 2. Transmission

- The encapsulated data (now called a packet) is transmitted over the physical medium to the receiving device.
- The **Physical Layer** converts the data into **bits (0s and 1s)**.
- These bits travel through the transmission medium (cable, Wi-Fi, fiber, etc.) to the destination.

```
Sender
   ↓
Bits (0s & 1s)
   ↓
Network Cable / Wi-Fi
   ↓
Receiver
```

## 3. Receiver's Side (Decapsulation)

- The receiver gets the bits at the **Physical Layer**.
- The data moves **upward** through the OSI layers.
- Each layer **removes its own header** (and the Data Link layer removes the trailer).
- This process is called **Decapsulation**.
- Finally, the original data reaches the **Application Layer**.

```
Physical (Receives Bits)
        ↑
Data Link (Removes Header + Trailer)
        ↑
Network (Removes Header)
        ↑
Transport (Removes Header)
        ↑
Session (Removes Header)
        ↑
Presentation (Removes Header)
        ↑
Application (Original Data Received)
```

This structured approach ensures data integrity and reliability, even over complex network.

---

# TCP/IP Model

The **TCP/IP Model** is a **4-layer networking model** that defines how data is transmitted between devices over a network or the Internet.

It provides a set of rules (protocols) that allow computers to communicate with each other reliably.

- To enable communication between different devices.
- To organize the data transmission process into layers.
- To ensure reliable and efficient data transfer over networks.
- It is the **practical model used on the Internet**, unlike the OSI model, which is mainly a reference model.
- Serves as the core framework of the modern Internet and networking systems.

## Layers of the TCP/IP Model

|Layer|Main Function|Example Protocols|
|---|---|---|
|**Application Layer**|Provides network services to user applications|HTTP, HTTPS, FTP, SMTP, DNS|
|**Transport Layer**|Ensures reliable communication and data delivery|TCP, UDP|
|**Internet Layer**|Handles logical addressing and routing|IP, ICMP, ARP|
|**Network Access Layer** (Link Layer)|Transmits data over the physical network|Ethernet, Wi-Fi, PPP|

## How the TCP/IP Model Works

1. The user sends data from an application (e.g., a web browser).
2. The **Application Layer** prepares the data for transmission.
3. The **Transport Layer** divides the data into segments and uses **TCP** or **UDP** for communication.
4. The **Internet Layer** adds the source and destination IP addresses and decides the best route.
5. The **Network Access Layer** converts the data into frames and transmits it as bits over the network.
6. The receiving device receives the data and processes it in the reverse order until it reaches the application.

# Difference Between OSI Model and TCP/IP Model

|**OSI Model**|**TCP/IP Model**|
|---|---|
|Developed by **ISO (International Organization for Standardization)**.|Developed by **DARPA (U.S. Department of Defense)**.|
|Has **7 layers**.|Has **4 layers**.|
|It is a **reference (theoretical) model** used to understand networking concepts.|It is a **practical model** used for communication on the Internet.|
|Layers are **Application, Presentation, Session, Transport, Network, Data Link, and Physical**.|Layers are **Application, Transport, Internet, and Network Access**.|
|Presentation and Session are **separate layers**.|Presentation and Session functions are included in the **Application Layer**.|
|Data Link and Physical are **separate layers**.|Data Link and Physical are combined into the **Network Access Layer**.|
|Clearly separates **services, interfaces, and protocols**.|Focuses mainly on **protocols** and practical communication.|
|More complex because it has more layers.|Simpler because it has fewer layers.|
|Mainly used for **learning, designing, and understanding** networks.|Used for **real-world Internet communication**.|
|Examples: Used in textbooks and networking education.|Examples: Used by protocols like **TCP, IP, HTTP, HTTPS, FTP, DNS**.|
## SOC Example (TCP/IP Mapping)

**Alert:** _Suspicious login via HTTPS from unknown IP_

- **Application Layer** → HTTPS login activity (user login request).
- **Transport Layer** → TCP **Port 443** (HTTPS communication).
- **Network Layer** → Source **IP address** (check if it's suspicious or unknown).
- **Data Link Layer** → Internal **MAC address/LAN device** (identify the affected host).