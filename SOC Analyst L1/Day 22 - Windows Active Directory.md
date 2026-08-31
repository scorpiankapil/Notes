# Windows Active Directory

**Windows Active Directory (AD)** is Microsoft's **centralized directory service** that centrally manages **users, computers, groups, devices, and permissions** within a Windows network.

**With AD:**

- All user information is stored once in a **central location** and every computer refers to that database.

- Centralized user management.
- User authentication.
- User authorization.
- Manage computers and devices.
- Apply security policies.
- Manage groups and permissions.
- Enable Single Sign-On (SSO).

## The Core Concept: Identity & Access

Active Directory performs **two main functions**:

#### 1. Authentication (Who are you?)

**Authentication** verifies your identity by checking your credentials (username/password).

**Example:**

- Username: `john`
- Password: `P@ssw0rd`
- AD checks if the password is correct.
- If correct → User is authenticated.

**Authentication = Verify Identity**

#### 2. Authorization (What can you access?)

**Authorization** determines what an authenticated user is allowed to do.

**Example:**

- John can access the **HR folder**.
- John cannot access the **Finance folder**.

**Authorization = Verify Permissions**

## Active Directory Components

| **Component**                   | **Definition**                                                                                                                                                   |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Object**                   | An **object** is an individual item stored in Active Directory, such as a **user, computer, printer, or group**.                                                 |
| **2. Organizational Unit (OU)** | An **OU** is a container used to **organize AD objects** into departments or groups, such as HR, Finance, or IT.                                                 |
| **3. Domain**                   | A **domain** is a logical security and administrative boundary that contains users, computers, groups, and other AD objects.                                     |
| **4. Domain Controller (DC)**   | A **Domain Controller** is a server that runs **Active Directory Domain Services (AD DS)** and handles authentication, authorization, and directory management.  |
| **5. Domain Tree**              | A **tree** is a collection of related domains that share a **continuous DNS namespace**.                                                                         |
| **6. Forest**                   | A **forest** is the largest logical structure in AD, containing **one or more domain trees** that share common AD configuration and schema.                      |
| **7. Site**                     | A **site** represents a **physical network location**, such as a branch office or data center, used mainly to optimize AD replication and network communication. |
| **8. Authentication**           | **Authentication** verifies **who a user or computer is**, such as checking credentials during login.                                                            |
| **9. Authorization**            | **Authorization** determines **what an authenticated user or computer is allowed to access or do** based on permissions.                                         |

**Authentication → "Who are you?"** 🔐  
**Authorization → "What can you access?"** 🔑

**OU → Organize**  
**Domain → Manage**  
**DC → Authenticate**  
**Tree → Group domains**  
**Forest → Group trees**

## How Active Directory Works

Think of **Active Directory (AD)** as a central system that manages **users, computers, groups, permissions, and security policies** in an organization.

```
Admin
  ↓
Creates Users / Computers / Groups
  ↓
Puts them into OUs (Organizational Units)
  ↓
Applies Group Policies (GPOs)
  ↓
Domain Controller (DC)
  ↓
Authenticates users + Enforces policies
  ↓
User gets access to allowed resources
```

- **Admin creates objects** → Users, computers, printers, and groups are created in AD.
- **Objects are organized** → Objects are placed inside **OUs (Organizational Units)** such as `HR`, `Finance`, or `IT`.
- **Groups are created** → Users are added to groups to make permission management easier.
- **Group Policies are applied** → GPOs define rules such as password requirements, desktop settings, and security restrictions.
- **Domain Controller manages everything** → The DC stores AD information and provides authentication and authorization.
- **User logs in** → The user's credentials are checked by the Domain Controller.
- **Permissions are checked** → AD determines what resources the user can access based on their groups and permissions.
- **Policies are enforced** → The appropriate GPOs are applied to the user's account and computer.

```
John (User)
    ↓
Finance OU
    ↓
Finance-Users Group
    ↓
Finance GPO
    ↓
Domain Controller
    ↓
Login verified
    ↓
Finance folder → ACCESS ✓
HR folder      → DENIED ✗
```

`Objects → OUs → Groups → GPOs → Domain Controller → Authentication → Authorization → Access`

# The Logical Structure (How it's Organized)
### 1. Objects 

An **object** is any individual item stored and managed in Active Directory.

- **Users:** People who log in
- **Computers:** The actual machine
- **Printers/Shared Folders:** Resources people need to use.

### 2. Organizational Units (OUs)

An **OU** is a container used to **organize AD objects** into departments or groups, such as HR, Finance, or IT.

An **OU** is a folder-like container used to organize AD objects.

```
Company
 ├── HR OU
 ├── Finance OU
 └── IT OU
```

### 3. Domains

A **domain** is a logical security boundary where users, computers, and resources are centrally managed.

**Example:** `corp.example.com`

### 4. Tree

A **tree** is a group of related domains that share a **contiguous DNS namespace**.

**Example:**

```
apple.com
   ├── sales.apple.com
   └── uk.apple.com
```

### 5. Forest

A **forest** is the highest-level logical structure in Active Directory that contains **one or more domain trees**.

```
Forest
 ├── Tree 1
 │    ├── Domain A
 │    └── Domain B
 │
 └── Tree 2
      ├── Domain C
      └── Domain D
```

# The Physical Structure (The Hardware)

While the logical structure is how you see it, the physical structure is where the **data actually lives.**

### 1. Domain Controller (DC):

- A **server that runs Active Directory Domain Services (AD DS)**.
- Stores the AD database (the file called`NTDS.dit`) and handles **authentication, authorization, and directory requests**.

**Site:**

- Represents a **physical network location**, such as a Delhi or London office.
- Helps AD choose nearby Domain Controllers and **optimize replication and authentication traffic**.

# Main Protocols Used by Active Directory

### 1. DNS (Domain Name System)

- Helps computers **find Domain Controllers and other services** using names.
- DNS acts as the **"phonebook of the Internet"**
- Example: A client uses DNS to find a DC for `corp.example.com`.

### 2. LDAP (Lightweight Directory Access Protocol)

- Used to **search and access information stored in Active Directory**.
- Example: Finding a user's account, group membership, or other directory information.

### 3. Kerberos

- The main **authentication protocol** used in modern Active Directory domains.
- After login, It uses **tickets** instead of sending the user's password repeatedly.
- Tickets allow users to access resources like **file servers, printers, and applications**.

---

### Group Policy 

- **Group Policy** is a feature of Active Directory used to **centrally apply rules and settings** to many computers and users.
- A **Group Policy Object (GPO)** contains the actual settings or rules.
- Administrators can apply one GPO to **hundreds or thousands of computers at once**.
- GPOs can be linked to a **Site, Domain, or OU**.
- Example: An administrator can configure all computers in the **Sales OU** to use the company wallpaper and automatically lock the screen after 5 minutes.
- Without Group Policy, the administrator would need to configure each computer **individually**.

**Example:**

```
Administrator
      ↓
    GPO
      ↓
  Sales OU
      ↓
 ┌────┼────┐
 PC-1 PC-2 PC-3
      ↓
 Same settings applied
```

Group Policy is a centralized way to apply rules and settings to multiple users and computers in an Active Directory environment.


## Kerberos Authentication in AD

- **User logs in** with username and password.
- **User requests a TGT** from the Domain Controller.
- **KDC verifies the user** and sends back a **TGT + Session Key**.
- When the user needs a resource, the computer **requests a Service Ticket** from the KDC.
- **KDC provides the Service Ticket + Session Key**.
- The user sends the **Service Ticket + Authenticator** to the Resource Server.
- **Resource Server validates the ticket**.
- If valid, the **server grants access** based on the user's permissions.

```
USER
  ↓
Request TGT
  ↓
DOMAIN CONTROLLER / KDC
  ↓
TGT + Session Key
  ↓
Request Service Ticket
  ↓
KDC
  ↓
Service Ticket
  ↓
RESOURCE SERVER
  ↓
ACCESS GRANTED
```

## 1. TGT (Ticket Granting Ticket)

- **TGT = Ticket Granting Ticket**
- It is a **ticket given to a user after successful Kerberos authentication**.
- It is issued by the **KDC (Key Distribution Center)** on the Domain Controller.
- It proves to the KDC that the user has **already authenticated**.
- The user uses the TGT to request **Service Tickets** for different network services.
- The TGT has a **limited lifetime**, so it is not valid forever. (Usually 10 hours)
- The TGT is **encrypted by the KDC**, so the user cannot normally modify it.

## 2. Session Key

- **Session Key** is a **temporary secret key** used by Kerberos to secure communication.
- It is generated during the Kerberos authentication process.
- It is used by the **client and the relevant server/service** to securely communicate.
- It is **temporary** and has a limited lifetime.
- It is **different from the user's password**.
- If the session ends or the key expires, a **new session key** can be generated. (Often expires after the task is done)
- Symmetric-key based

# Active Directory Attacks

| Attack                   | Simple meaning                                                                                                                            |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Pass-the-Hash (PtH)**  | Attacker uses a stolen **NTLM password hash** to authenticate without knowing the actual password.                                        |
| **Kerberoasting**        | Attacker requests **Kerberos service tickets** and attempts to crack the encrypted ticket material to recover a service account password. |
| **Golden Ticket**        | Attacker abuses a stolen `krbtgt` account secret to create forged Kerberos **TGTs**, potentially giving broad domain access.              |
| **DCSync**               | Attacker abuses replication privileges to make a **Domain Controller provide password-related secrets/hashes** for accounts.              |
| **Privilege Escalation** | Attacker gains higher privileges, e.g. compromising an account and getting it added to **Domain Admins**.                                 |