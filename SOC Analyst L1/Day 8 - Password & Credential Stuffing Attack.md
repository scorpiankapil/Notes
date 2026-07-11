# Password & Credential Stuffing Attack

A Credential Stuffing Attack is a type of password attack in which attackers use **stolen usernames and passwords** from previous data breaches to try logging into other websites or applications.

It succeeds because many users **reuse the same password** across multiple accounts.

# Types of Password Attacks

# 1. Brute Force Attack

A Brute Force Attack is a password attack in which an attacker tries **every possible password combination** until the correct password is found.

It is an automated attack that uses scripts or tools to guess passwords.

##### How a Brute Force Attack Works

- Attacker target a login portal (VPN, RDP, Web App)
- Sends thousands of password attempts
- If the correct password is found, the attacker gains access.

##### SOC Indicators of a Brute Force Attack

- **Event ID 4625 (Failed Logon)** – Multiple failed login attempts are recorded.
- **Multiple Login Attempts from the Same IP Address** – A single IP repeatedly tries to authenticate.
- **Same Username Targeted Repeatedly** – One account (e.g., _administrator_) receives many failed login attempts.
- **High Number of Failed Logins in a Short Time** – Hundreds or thousands of failed logins within minutes.
- **Account Lockout Events (Event ID 4740)** – The account is locked after too many failed attempts.

##### In Firewall / VPN Logs

- Correlation rule triggers for excessive failed logins.
- Brute-force detection alerts.
- Spike in authentication events.
- Multiple failed logins followed by one successful login (possible compromise).

## Types of Brute Force Attack

#### 1. Simple Brute Force Attack

The attacker tries **every possible password combination** until the correct password is found.

**Example:** 

```
Password1
Password12
Password123
Password1234
...
```

#### 2. Dictionary Attack

The attacker uses a **predefined list (dictionary)** of common passwords instead of trying every possible combination.

**Example:**

```
password
123456
admin
welcome
qwerty
Password@123
```

#### 3. Reverse Brute Force Attack

A Reverse Brute Force Attack tries one known common password on many different user accounts.

- The attacker uses **one common password against many usernames**.

**Example:** 

```
Password: Welcome@123

admin
rahul
kapil
john
alice
```

#### 4. Password Spraying Attack

A Password Spraying Attack is a type of password attack in which an attacker tries **one or a few common passwords against many different user accounts**.

Suppose an attacker has these usernames:

```
kapil
rahul
john
alice
admin
```

The attacker tries **one password**:

```
Welcome@123
Password@123
Spring2025!
```

| Password Spraying                                                       | Reverse Brute Force Attack                                         |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Tries **one or a few common passwords** against many user accounts.     | Tries **one known password** against many user accounts.           |
| Uses common passwords like `Password123`, `Welcome@123`, `Spring2025!`. | Uses a specific password obtained or chosen by the attacker.       |
| Goal is to find users with weak/common passwords.                       | Goal is to find users who use that particular password.            |
| Commonly seen in enterprise attacks.                                    | Less common term; often considered a subtype of password spraying. |

#### 5. Hybrid Attack

A Hybrid Attack is a password attack that combines common dictionary words with numbers, symbols, or characters to guess passwords.

**Common Dictionary Words + Numbers, Symbols, or Characters = Hybrid Attack**

**Example:**

Dictionary words:

```
admin
password
welcome
summer
```

The attack tool generates:

```
Admin123
admin@123
Password123
Welcome2025
Summer@2025
password1
```

If the user's password is **Welcome2025**, the attacker successfully logs in.

# 2. Rainbow Table Attack

A Rainbow Table Attack is a password attack in which an attacker uses **precomputed tables of password hashes** (called rainbow tables) to quickly find the original password from a stolen password hash.

Instead of guessing passwords one by one, the attacker looks up the hash in a rainbow table.

**Example:**

```
Password: admin123
Hash:0192023a7bbd73250516f069df18b500
```

The website stores the **hash**, not the password.

- Ophcrack is a free Windows password cracker based on rainbow tables.
- Cracks LM and NTLM hashes.
- https://ophcrack.sourceforge.io/

# 3. Credential Stuffing

Credential Stuffing is a password attack in which attackers use **stolen usernames and passwords** from previous data breaches to log in to other websites or applications.

It works because many people **reuse the same username and password** across multiple accounts.

**Example:**

A data breach exposes these credentials:

```
Username: kapil@gmail.com
Password: kapil@123
```

The attacker tries the same credentials on:

- Gmail
- Facebook
- Instagram
- Amazon

If the user uses **kapil@123** on these websites, the attacker can log in.

# 4. MFA Fatigue Attack

An MFA Fatigue Attack is a cyberattack in which an attacker repeatedly sends **Multi-Factor Authentication (MFA) approval requests** to a user's device until the user becomes frustrated or confused and accidentally approves one of them.

It is also called **Push Bombing** or **MFA Prompt Bombing**.

**Example:**

An attacker has your password and tries to log in.

Your phone receives notifications like:

```
MFA RequestApprove?  Yes / No
```

You receive **20–30 notifications** in a few minutes.

Thinking it's a system error or by accidentally tapping **Approve**, you approve one request.

The attacker immediately logs into your account.

---

# SOC L1 Investigation Workflow

### Alert Received

```
"Multiple Failed Login Attempts"
```

As a **SOC L1 Analyst**, you should investigate the following:

1. Check the Source IP
2. Check the Geolocation
3. Check the Username Targeted
4. Check Success or Only Failures?
5. Check Time Frequency
6. Account lockout triggered?
7. Check for Successful Login After Failures

**If yes ---> escalate immediately**

### Important Logs to Check

#### Windows Event Logs

|Event ID|Description|
|---|---|
|**4625**|Failed Login|
|**4624**|Successful Login|
|**4776**|NTLM Authentication|
|**4740**|Account Lockout|
#### Linux Logs

|Log File|Purpose|
|---|---|
|**/var/log/auth.log**|Authentication and login events|
|**SSH Logs**|SSH login attempts (successful and failed)|

#### Firewall Logs

- Repeated connection attempts.
- Blocked connection spikes.
- Authentication failures.
- Multiple connections from the same IP.

## Prevention Mechanism

- Account lockout policy
- MFA enforcement
- Rate limiting
- CAPTCHA
- Geo-blocking
- Strong password policy
- Disable default accounts