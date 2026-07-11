# Phishing

Phishing is a social engineering attack in which attackers trick people into revealing sensitive information, such as usernames, passwords, credit card details, or banking information, by pretending to be a trusted person or organization.

https://isitphishing.org/
https://phishtank.com/

##### How Phishing Works

1. The attacker creates a fake email, website, or message.
2. The victim receives the phishing message.
3. The victim clicks a malicious link or opens an attachment.
4. The victim enters sensitive information or downloads malware.
5. The attacker steals the information or compromises the system.

##### SOC Detection

- **Email from Spoofed Domain:** The email is sent from a fake sender address that impersonates a trusted organization.
- **Domain Looks Similar (Typosquatting):** The sender uses a lookalike domain (e.g., **micr0soft.com**) to deceive users.
- **Suspicious Attachments:** The email contains potentially malicious files such as **.zip, .html, .exe, .docm, .js**, or **.iso**.
- **URL Redirect Chains:** The email link passes through multiple redirects to hide the malicious destination.
- **SPF Failure:** The sender's mail server is not authorized to send emails for the claimed domain.
- **DKIM Failure:** The email's digital signature is invalid or missing, indicating possible tampering.
- **DMARC Failure:** The email fails domain authentication checks, indicating it may be spoofed or fraudulent.

---
## `SPF, DKIM, and DMARC Authentication`

`SPF, DKIM, and DMARC are **email authentication protocols** that help verify whether an email is genuine or fake. They are used to protect against **email spoofing** and **phishing attacks**.`

### `1. SPF (Sender Policy Framework)`

`SPF is an email authentication protocol that verifies whether the email was sent from an **authorized mail server** for the claimed domain.`

- `The receiving mail server checks the domain's SPF record.`
- `It verifies whether the sending mail server is authorized.`
- `If authorized → **SPF Pass**.`
- `If not authorized → **SPF Fail**.`

### `2. DKIM (DomainKeys Identified Mail)`

`DKIM is an email authentication protocol that adds a **digital signature** to an email to verify that the message has not been modified during transmission.`

- `The sender's mail server adds a digital signature.`
- `The receiving server verifies the signature.`
- `If the signature matches → **DKIM Pass**.`
- `If it doesn't match → **DKIM Fail**.`

### `3. DMARC (Domain-based Message Authentication, Reporting, and Conformance)`

`DMARC is an email authentication protocol that uses the results of SPF and DKIM to determine whether an email should be accepted, quarantined, or rejected by the receiving mail server.`

- `The receiving server checks SPF.`
- `It checks DKIM.`
- `DMARC evaluates the results.`
- `Based on the domain's DMARC policy, the email is:`
    - `Accepted`
    - `Quarantined (sent to spam)`
    - `Rejected`

---
# Types of Phishing 

# 1. Spear Phishing

Spear phishing is a targeted phishing attack in which an attacker sends a personalized email, message, or communication to a specific individual or organization to steal sensitive information or install malware.

- Looks extremely legitimate
- Often bypasses spam filters
- High financial damage
###### Example

A finance employee receives an email:

```
 Hi Rahul,
 Please review the attached invoice before today's meeting.
 – Finance Manager
```

The attachment contains malware that installs on the employee's computer.

This is a **Spear Phishing** attack because it is **personalized and targets a specific person**.

# 2. Whaling

Whaling is a type of phishing attack that specifically targets high-profile individuals such as CEOs, CFOs, directors, senior managers, and other executives to steal sensitive information or commit financial fraud.

It is also known as **CEO Fraud** or **Executive Phishing**.

##### Example

The CFO receives an email that appears to be from the CEO:

```
"I'm in a meeting. Please transfer ₹25,00,000 to this account immediately. This is confidential."
```

The CFO transfers the money without verifying the request.

This is a **Whaling attack** because it specifically targets a senior executive.

# Smishing

Smishing (SMS Phishing) is a type of phishing attack in which attackers use **SMS (text messages)** to trick victims into revealing sensitive information, clicking malicious links, or downloading malware.

The word **Smishing** comes from:

- **SMS** + **Phishing** = **Smishing (Phishing via SMS)**

##### Example

You receive an SMS:

```
"Your bank account has been blocked. Click here to verify your account: bank-secure-login.com"
```

You click the link and enter your username, password, and OTP.

The attacker steals your banking credentials.

This is a **Smishing attack**.

# Vishing 

Vishing (Voice Phishing) is a type of phishing attack in which attackers use **phone calls or voice messages** to trick victims into revealing sensitive information, such as passwords, OTPs, banking details, or personal information.

The word **Vishing** comes from:

- **Voice** + **Phishing** = **Vishing (Phishing via Phone Call)**

##### Example

You receive a phone call:

```
"Hello, this is your bank. Your account has been blocked. Please tell me the OTP sent to your phone to verify your account."
```

You share the OTP.

The attacker uses it to access your bank account.

This is a **Vishing attack**.

# Pharming

Pharming is an attack where the victim is redirected to a fake website even if they type the correct website address.

It is a cyberattack that secretly redirects users from a legitimate website to a fake website to steal sensitive information.

##### Example

You type:

```
www.mybank.com
```

Instead of opening the real bank website, you are secretly redirected to a fake website that looks exactly like the original.

You enter:

- Username
- Password
- OTP

The attacker steals your banking credentials.

This is a **Pharming attack**.

## Method 1 - DNS Poisoning

DNS Poisoning is a cyberattack in which an attacker inserts false or malicious DNS records into a DNS server or DNS cache, causing users to be redirected to a fake or malicious website instead of the legitimate one.

- DNS Server
- Local router

##### Working of DNS Poisoning

- The attacker compromises a **DNS server** or **DNS cache** by inserting fake DNS records.
- The user enters the correct website address (e.g., **www.bank.com**) in the browser.
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


## Method 2 - Host File Modification

Host File Modification is a technique where an attacker changes the **hosts file** on a computer to redirect a legitimate website to a fake or malicious IP address.

```
C:\Windows\System32\drivers\etc\hosts
```

- The **hosts file** is a local file on your computer that maps **domain names** to **IP addresses**.
- Before your computer asks a DNS server, it checks the **hosts file** first.

###### How Host File Modification Works

1. The attacker gains access to the victim's computer.
2. The attacker modifies the **hosts** file.
3. A fake IP address is mapped to a legitimate website.
4. The user enters the correct website address.
5. The computer checks the hosts file first and uses the fake IP address.
6. The user is redirected to the attacker's fake website.

##### Example

**Original Hosts File**

```
127.0.0.1       localhost
```

**Modified Hosts File**

```
203.0.113.50    www.bank.com
```

Now, whenever the user types:

```
www.bank.com
```

the computer goes to **203.0.113.50** (the attacker's fake website) instead of the real bank website.

### SOC Detection Indicators

1. Sudden DNS Record Changes
2. Suspicious DNS Responses
3. Unusual DNS behavior or unauthorized changes detected within the organization's DNS infrastructure.
4. Host File Modification Alerts
5. Multiple Users Resolving the Same Domain to an Unusual IP
6. Certificate Mismatch Errors

### Real SOC Scenario

##### Alert

```
Multiple users accessing `bank.com` are being redirected to an unknown foreign IP address.
```

This suggests a possible **DNS Poisoning** or **Pharming** attack.

##### SOC Investigation Steps

1. Check DNS Logs
2. Compare with Known Legitimate IP
3. Check for DNS Server Compromise
4. Check Endpoints for Hosts File Tampering

# Evil Twin Attack

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

##### SOC Detection of Evil Twin Attack

- Detect unauthorized or rogue access points.
- Monitor duplicate or similar SSIDs.
- ARP Spoofing alerts
- Unusual DHCP server detected
- Network traffic interception pattern

##### Enterprise SOC teams use:

- Wireless IDS (WIDS)
- Network Access Control (NAC)
- Certified-based WiFi auth (802.1X)

---
# Social Engineering

Social Engineering is a technique used by attackers to manipulate, deceive, or trick people into revealing sensitive information or performing actions that compromise security.

- It exploit human vulnerabilities, not technical vulnerabilities

# Types of Social Engineering

# 1. Pretexting

