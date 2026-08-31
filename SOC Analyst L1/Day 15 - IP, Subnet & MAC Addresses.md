# IP Address (Internet Protocol Address)

An **IP Address (Internet Protocol Address)** is a unique logical address assigned to a device on a network. It helps identify the source and destination of data so that devices can communicate with each other over a network or the Internet.

- Identifies devices on a network
- Enables communication between devices
- Helps routers forward packets to the correct destination
- Provides logical addressing
- Supports Internet connectivity

## Why is an IP Address Needed?

An **IP address** is needed because every device on a network must have a unique identifier so that data can be sent to and received from the correct device.

Without IP addresses, computers, phones, and servers would not know where to send data or where data is coming from.

When data is sent over a network, the IP Address knows:

- Who is sending the data?
- Who should receive the data

# IPv4 and IPv6

## 1. IPv4 (Internet Protocol Version 4)

**IPv4** is the older and most widely used version of the Internet Protocol. It uses a **32-bit address** to identify devices on a network

- Uses 32-bit addresses
- Supports about 4.3 billion unique addresses
- Written in decimal format
- Consists of 4 octets separated by dots
- 1 octet = 8bits/ 1byte
- 4 x octet = 4 x 8 = 32bits / 4bytes

**Example:** 
- 192.168.1.10

## 2. IPv6 (Internet Protocol Version 6)

**IPv6** is the newer version of the Internet Protocol designed to overcome the shortage of IPv4 addresses. It uses a **128-bit address** and provides a much larger address space.

- Uses 128-bit addresses
- Supports an extremely large number of addresses
- Written in hexadecimal format
- Consists of 8 groups separated by colons

**Example:**
- 2001:db8::1

# Two types of IP Addresses

## 1. Public IP Address

A **Public IP Address** is assigned by an Internet Service Provider (ISP) and is used to communicate over the Internet. It is globally unique and can be accessed from anywhere on the Internet.

- Internet access
- Hosting websites and servers
- Online communication

Example: 
- 103.21.45.12

## 2. Private IP Address

A **Private IP Address** is used within a local network (LAN) and cannot be accessed directly from the Internet. It is assigned by a router or DHCP server.

- Home networks
- Office networks
- Internal device communication

Example: 
- 192.168.1.10
- 10.0.0.5
- 172.16.1.20

# Why Was IPv6 Introduced?

**IPv6 was introduced because IPv4 was running out of available IP addresses.** With the rapid growth of the Internet, smartphones, computers, IoT devices, and servers required more unique IP addresses than IPv4 could provide.

IPv6 was developed to solve this problem by offering a much larger address space and improved networking features.

### Reasons for Introducing IPv6

- IPv4 supports only about **4.3 billion addresses**.
- The number of Internet-connected devices grew rapidly.
- IPv6 provides a **much larger address space (128-bit addresses)**.
- Improves routing efficiency.
- Offers better built-in security support.
- Supports automatic IP address configuration.

---

# Subnet Mask

A **Subnet Mask** is a 32-bit number used with an IPv4 address to identify which part of the IP address represents the **network** and which part represents the **host (device)**.


A Subnet Mask is a number that tells us:

- Which part of the IP address is the **Network ID**
- Which part of the IP address is the **Host ID**

Without a subnet mask, a computer cannot determine:

- Whether the destination device is on the same network
- Or on a different network

**Example -** 
 
 - IP Address
 
```
192.168.1.10
```

 - Subnet Mask

```
255.255.255.0
```

- In this case
    - 192.168.1 identifies the network and
    - 10 identifies the specific device on network

## Common Subnet Masks

| Subnet Mask     | CIDR | Meaning                        | Usable Port |
| --------------- | ---- | ------------------------------ | ----------- |
| 255.0.0.0       | /8   | First 8 bits are network bits  | 16,777,214  |
| 255.255.0.0     | /16  | First 16 bits are network bits | 65,534      |
| 255.255.255.0   | /24  | First 24 bits are network bits | 254         |
| 255.255.255.192 | /26  | First 26 bits are network bits | 62          |
| 255.255.255.224 | /27  | First 27 bits are network bits | 30          |

# What is Subnet?

A **Subnet (Subnetwork)** is a smaller network created from a larger network. It allows a large network to be divided into multiple smaller and manageable networks.

In a large network, all devices share the same broadcast domain, which can increase traffic and reduce performance. By creating subnets, devices are grouped into smaller networks, reducing unnecessary traffic and improving efficiency.

## Example of a Subnet

Suppose we have the network:

```
192.168.1.0/24
```

This network can support **254 hosts**.

If a company has different departments:

- HR Department
- Finance Department
- IT Department
- Management Department

Instead of putting all devices in one network, the company can create separate subnets for each department.

# What is Subnetting?

**Subnetting** is the process of dividing a large IP network into multiple smaller networks called subnets by modifying the subnet mask and borrowing bits from the host portion of the IP address.

- Reduces network traffic
- Improves network performance
- Enhances security
- Makes network management easier
- Uses IP addresses more efficiently

# Subnet vs Subnetting

|Subnet|Subnetting|
|---|---|
|A **Subnet** is a smaller network created from a larger network.|**Subnetting** is the process of dividing a larger network into smaller networks.|
|It is the **result** of subnetting.|It is the **method/process** used to create subnets.|
|Represents a network segment.|Represents a network design technique.|
|Used to organize devices into smaller groups.|Used to improve performance, security, and IP address management.|
|Example: `192.168.1.0/26`|Example: Dividing `192.168.1.0/24` into four `/26` networks.|
- **Subnetting** = Dividing the school into different classrooms.
- **Subnet** = Each classroom created after the division.

---

# CIDR (Classless Inter-Domain Routing)

**CIDR (Classless Inter-Domain Routing)** is a method of IP addressing that allows networks to be divided into flexible sizes using a prefix length (e.g., `/24`, `/26`, `/16`).

It replaces the old classful addressing system and helps use IP addresses more efficiently.

- Reduces IP address wastage
- Supports subnetting
- Flexible network sizes
- Improves routing efficiency
- Replaces classful addressing

## Why is CIDR Needed?

In classful addressing:

- Class A → Very large network
- Class B → Medium network
- Class C → Small network

Many IP addresses were wasted because network sizes were fixed.

CIDR solves this by allowing network administrators to create networks of any size they need.

## CIDR Notation

CIDR uses a slash (`/`) followed by a number.

### Example

```
192.168.1.0/24
```

Here:

- `192.168.1.0` = Network Address
- `/24` = First 24 bits are Network Bits

## Common CIDR Values

**Formula to calculate Usable Hosts:**

Total IPs = 2^(32 - subnet prefix)
Total IPs = 2^(32 - 24) = 256

|CIDR|Subnet Mask|Usable Hosts|
|---|---|---|
|/8|255.0.0.0|16,777,214|
|/16|255.255.0.0|65,534|
|/24|255.255.255.0|254|
|/26|255.255.255.192|62|
|/27|255.255.255.224|30|

# How CIDR Works

CIDR works by specifying **how many bits of an IP address are used for the Network ID**. The remaining bits are used for **Host IDs**.

The CIDR number is written after a slash (`/`).

## Example 1: /24

```
192.168.1.0/24
```

This means:

- 24 bits = Network Part
- 8 bits = Host Part

|Network ID|Host ID|
|---|---|
|192.168.1|0-255|

Usable Hosts:

**2⁸ - 2 = 254 hosts**


## Example 2: /26

```
192.168.1.0/26
```

This means:

- 26 bits = Network Part
- 6 bits = Host Part

|Network ID|Host ID|
|---|---|
|192.168.1|Last 6 bits|

Usable Hosts:

**2⁶ - 2 = 62 hosts**


## What Happens When CIDR Number Increases?

|CIDR|Hosts|
|---|---|
|/24|254|
|/25|126|
|/26|62|
|/27|30|

As the CIDR number **increases**:

- More bits are used for the network.
- Fewer bits remain for hosts.
- The network becomes smaller.

### Simple Example

Suppose a company needs only 50 devices.

Using:

```
192.168.1.0/24
```

gives 254 hosts (many wasted).

Using:

```
192.168.1.0/26
```

gives 62 hosts (almost perfect).

CIDR allows you to choose the exact network size you need.

```
Higher CIDR (/26, /27)
      ↓
More Network Bits
      ↓
Fewer Host Bits
      ↓
Smaller Network
```

---

# IP Address classes

**Address Classes** are categories of IPv4 addresses that divide the IP address space into different ranges based on network size and number of hosts.

IPv4 addresses are divided into **Class A, B, C, D, and E**.

# Class A Addresses

A **Class A address** is a type of IPv4 address designed for very large networks. It uses the first octet for the network ID and the remaining three octets for host IDs.

- Use for Large networks
- Government Organizations

- **First Octet:** 1 to 126
- **IP Range:** `1.0.0.0` to `126.255.255.255`

### Default Subnet Mask

```
255.0.0.0
```

| Octet     | Portion    |
| --------- | ---------- |
| 1st Octet | Network ID |
| 2nd Octet | Host ID    |
| 3rd Octet | Host ID    |
| 4th Octet | Host ID    |
### Example 

**IP Address**

```
12.56.87.34
```

 **Subnet Mask**

```
255.0.0.0
```

**Result:**

```
Network ID = 12
Host ID = 56.87.34
```

**This means:**

- Device belongs to Network 12
- Host number is 56.87.34

`127 is reserved for loopback`
# Class B Addresses

A Class B address is an IPv4 address where the **first octet ranges from 128 to 191**. It is designed for **medium-sized networks** because it supports a large number of hosts while allowing more networks than Class A.

- Medium-sized network
- Used in universities

- **First Octet:** 128 to 191
- **IP Range:** `128.0.0.0` to `191.255.255.255`

### Default Subnet Mask

```
255.255.0.0
```

| Octet     | Portion    |
| --------- | ---------- |
| 1st Octet | Network ID |
| 2nd Octet | Network ID |
| 3rd Octet | Host ID    |
| 4th Octet | Host ID    |
### Example

**IP Address**

```
172.16.87.34
```

**Subnet Mask**

```
255.255.0.0
```

**Result:**

```
Network ID = 172.16
Host ID = 87.34
```

**This means:**

- Device belongs to **Network 172.16**
- Host number is **87.34**

# Class C Addresses

A **Class C address** is a type of IPv4 address designed for **small networks**. It uses the **first three octets for the Network ID** and the **last octet for the Host ID**.

- Class C addresses are the most commonly used addresses in home and small office networks.
- Small network

- **First Octet:** 192 to 223
- **IP Range:** `192.0.0.0` to `223.255.255.255`

### Default Subnet Mask

```
255.255.255.0
```

### Example

**IP Address**

```
192.168.1.10
```

**Subnet Mask**

```
255.255.255.0
```

**Result**

```
Network ID = 192.168.1Host ID = 10
```

**This Means**

- Device belongs to **Network 192.168.1**
- Host number is **10**

# Class D Addresses 

A **Class D address** is a special type of IPv4 address used for **multicasting**. It is not assigned to individual devices like Class A, B, or C addresses.

Multicasting allows one sender to send data to multiple devices (a group) at the same time.

- **First Octet:** 224 to 239
- **IP Range:** `224.0.0.0` to `239.255.255.255`

### Default Subnet Mask

**No default subnet mask**

- Class D addresses are not used for normal host addressing.

### Purpose of Class D

Used for **Multicast Communication**.

Instead of sending the same data separately to many devices, one packet is sent to a multicast group, and all members of that group receive it.

### Example

Suppose a company is broadcasting a live video to 100 employees.

#### Without Multicast

- Server sends 100 separate streams.

#### With Multicast (Class D)

- Server sends 1 stream to a multicast address.
- All 100 employees receive the stream.

This saves bandwidth and improves efficiency.

# Class E Addresses

A **Class E address** is a special type of IPv4 address reserved for **research, testing, and experimental purposes**. These addresses are not used for normal communication between devices on a network.

- **First Octet:** 240 to 255
- **IP Range:** `240.0.0.0` to `255.255.255.255`

### Default Subnet Mask

**No default subnet mask**

- Class E addresses are not used for host addressing.

### Purpose of Class E

- Research and development
- Network experiments
- Future use and testing

# IPv4 Addresses Classes

| Class              . | First Octet Range | IP Address Range            | Default Subnet Mask | CIDR | Purpose                       |
| -------------------- | ----------------- | --------------------------- | ------------------- | ---- | ----------------------------- |
| **Class A**          | 1 - 126           | 1.0.0.0 - 126.255.255.255   | 255.0.0.0           | /8   | Large networks                |
| **Class B**          | 128 - 191         | 128.0.0.0 - 191.255.255.255 | 255.255.0.0         | /16  | Medium-sized networks         |
| **Class C**          | 192 - 223         | 192.0.0.0 - 223.255.255.255 | 255.255.255.0       | /24  | Small networks                |
| **Class D**          | 224 - 239         | 224.0.0.0 - 239.255.255.255 | N/A                 | N/A  | Multicasting                  |
| **Class E**          | 240 - 255         | 240.0.0.0 - 255.255.255.255 | N/A                 | N/A  | Research and Experimental Use |

---

# MAC Address

A MAC Address (Media Access Control Address) is a unique physical address assigned to every network card (NIC) by the manufacturer.

It is used to identify devices on a local network.

The MAC address is stored (burned) into the network card hardware.

## MAC Address Format

A MAC address is:

- 48-bit address
- Written in hexadecimal format
- Contains 12 hexadecimal characters

### Example

- 00-90-4B-4C-C1-59
- 00:90:4B:4C:C1:59

## Structure of MAC Address

The MAC address has two parts:

| Part               | Purpose          |
| ------------------ | ---------------- |
| First 6 characters | Manufacturer ID  |
| Last 6 characters  | Unique device ID |

Example: 00-90-4B-4C-C1-59

|Section|Value|Description|
|---|---|---|
|OUI (Manufacturer ID)|00-90-4B|Identifies the manufacturer/vendor|
|Device Identifier|4C-C1-59|Identifies the specific device uniquely|

## How to View MAC Address

### Windows

Command:

```
ipconfig /all
```

MAC address appears as:

- Physical Address

### Linux

Command:

```
ifconfig
```
