# IP / Data Packets

A **data packet** is a **small unit of data** that travels across a network from a source device to a destination device.

Large files or messages are **split into small packets** before being sent over a network and that process is **fragmentation or packetization**.

An IP packet is the basic unit of data transmission at the Network Layer. It contains an IP header with routing information (such as source and destination IP addresses) and a payload containing the actual data. Routers use the destination IP address in the header to forward the packet across the network.

- **Header** - Control info
- **Payload**  - Actual Data

#### Packet Encapsulation

**Packet Encapsulation** is the process of **adding protocol information to data (headers and sometimes trailers)** at each network layer **(OSI or TCP/IP layers)** before being transmitted over a network.

- Data moves through each layer
- Each layer adds its own header

## Structure of an IP Packet

```
+------------------------------------+
|            IP Header               |
| Source IP                          |
| Destination IP                     |
| TTL                                |
| Protocol                           |
| Total Length                       |
| Version                            |
+------------------------------------+
|            Payload                 |
|          Actual Data               |
+------------------------------------+
```

- **Version** – Specifies the IP version (**IPv4** or **IPv6**).
- **Total Length** – Indicates the total size of the IP packet (header + data).
- **Protocol** – Identifies the transport protocol carried in the packet (e.g., **TCP**, **UDP**, **ICMP**).
- **Time To Live (TTL)** – Limits how many routers the packet can pass through before being discarded or How long can the packet travel?
- **Source IP Address** – Contains the IP address of the sender.
- **Destination IP Address** – Contains the IP address of the intended receiver.
- **Header** – Stores routing and control information needed to deliver the packet.
- **Payload (Data)** – Contains the actual data.

### IPv4 Header Fields (Layer 3 - Network Layer)

| **Field**                  | **Meaning**                                                                  | **SOC Use**                                                   |
| -------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **Version**                | Indicates the IP version (**IPv4** or **IPv6**).                             | Identifies the IP protocol version being used.                |
| **Source IP Address**      | IP address of the sender.                                                    | Helps identify the attacker or source of suspicious traffic.  |
| **Destination IP Address** | IP address of the receiver.                                                  | Identifies the target system or destination host.             |
| **TTL (Time To Live)**     | Number of hops a packet can travel before being discarded or packet lifetime | Detects routing anomalies, loops, and suspicious packets.     |
| **Protocol**               | Specifies the transport protocol (**TCP, UDP, ICMP**, etc.).                 | Identifies the type of network traffic.                       |
| **Total Length**           | Total size of the IP packet (header + payload).                              | Detects abnormal packet sizes and possible data exfiltration. |
| **Header Checksum**        | Verifies the integrity of the IP header.                                     | Detects packet corruption or header manipulation.             |

### TCP Header Fields (Layer 4 - Transport Layer)

|**Field**|**Meaning**|**SOC Use**|
|---|---|---|
|**Source Port**|Port number of the sender (client).|Identifies the origin of the connection or traffic.|
|**Destination Port**|Port number of the target service (e.g., 80, 443, 22).|Detects which service is being accessed or attacked.|
|**Sequence Number**|Tracks the order of TCP packets for reliable delivery.|Used for session analysis and packet reassembly.|
|**ACK (Acknowledgment) Number**|Confirms receipt of previously received data.|Validates TCP communication flow and detects anomalies.|
|**Flags**|Indicates the connection state (SYN, ACK, FIN, RST, PSH, URG, etc.).|Detects attacks such as SYN floods, scans, and abnormal TCP behavior.|
|**Window Size**|Specifies how much data can be received before an acknowledgment is required (flow control).|Analyzes traffic behavior, congestion, and performance issues.|

#### TTL - Time To Live

**Time To Live (TTL)** is an IPv4 header field that defines how long an IP packet remains valid by specifying the maximum number of routers (hops) it can traverse before it expires and is discarded. This prevents packets from looping indefinitely and ensures efficient network communication.

- When the **TTL (Time To Live) value becomes 0**, the IP packet is **immediately discarded (dropped)** by the router.

- A packet starts with a TTL value (e.g., 64).
- Each router decreases the TTL by **1**.
- When the TTL reaches **0**:
    - The router **discards the packet**.
    - The router usually sends an **ICMP Time Exceeded** message back to the sender.

```
C:\Users\scorp>tracert -4 facebook.com

Tracing route to facebook.com [57.144.150.1]
over a maximum of 30 hops:

  1    10 ms     9 ms     9 ms  104.28.0.0
  2    10 ms    10 ms     *     172.69.118.33
  3    11 ms    10 ms    11 ms  104.23.231.10
  4    58 ms     *        *     198.41.162.67
  5    96 ms    96 ms    96 ms  198.41.161.145
  6    96 ms    96 ms    96 ms  172.69.117.33
  7    97 ms    97 ms    97 ms  ae90.pr02.sin6.tfbnw.net [157.240.74.144]
  8    96 ms    96 ms    96 ms  po4001.asw02.sin11.tfbnw.net [129.134.107.210]
  9    96 ms    96 ms    96 ms  usw02.sin11.tfbnw.net [129.134.95.164]
 10    99 ms    99 ms    99 ms  163.77.195.60
 11    96 ms    96 ms    96 ms  edge-star-mini-shv-02-sin11.facebook.com [57.144.150.1]
```

#### How Does TTL Work?

1. A computer sends an IP packet with a **TTL value** (e.g., **64**).
2. The packet reaches the **first router**.
3. The router decreases the TTL by **1**.
4. The packet is forwarded to the next router.
5. Every router repeats this process by reducing the TTL by **1**.
6. If the packet reaches its destination before the TTL becomes **0**, it is delivered successfully.
7. If the TTL becomes **0** before reaching the destination, the router **drops the packet** and usually sends an **ICMP Time Exceeded** message to the sender.


# 3 Way Handshake

The **TCP 3-Way Handshake** is a fundamental process used in the Transmission Control Protocol (TCP) to establish a reliable connection between a client and a server before data transmission begins. This handshake ensures that both parties are synchronized and ready for communication.

- Ensures both devices are ready to communicate.
- Synchronizes sequence numbers.
- Creates a reliable TCP connection.

```
Step 1:
Client ------------------ SYN ------------------> Server

Step 2:
Client <-------------- SYN + ACK --------------- Server

Step 3:
Client ------------------ ACK ------------------> Server

✅ TCP Connection Established
```


#### Working of TCP 3-Way Handshake

1. Client sends a **SYN** packet to request a connection.
2. Server responds with **SYN-ACK** to acknowledge the request.
3. Client sends an **ACK** to confirm.
4. TCP connection is established.
5. Data transfer begins.

| **Flag** | **Full Form**  | **Purpose**                                                                                         |
| -------- | -------------- | --------------------------------------------------------------------------------------------------- |
| **SYN**  | Synchronize    | Requests a new TCP connection and synchronizes sequence numbers.                                    |
| **ACK**  | Acknowledgment | Confirms that a packet has been received successfully.                                              |
| **FIN**  | Finish         | Gracefully terminates an existing TCP connection.                                                   |
| **RST**  | Reset          | Immediately terminates a TCP connection due to an error or invalid request.                         |
| **PSH**  | Push           | Instructs the receiver to deliver the received data to the application immediately without waiting. |
| **URG**  | Urgent         | Indicates that the packet contains urgent data that should be processed first.                      |
##### Easy Analogy

Imagine making a phone call 📞:

- **SYN:** "Hello, can we talk?"
- **SYN-ACK:** "Yes, I can hear you. Can you hear me?"
- **ACK:** "Yes, I can hear you too."

Now both people start talking.

