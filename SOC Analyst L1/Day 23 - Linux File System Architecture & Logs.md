# Linux File System

The **Linux file system** is the way Linux **organizes and stores files, directories, programs, and system data**.

Linux uses **one main directory tree starting from `/` (root)**.

|Directory|Simple meaning|
|---|---|
|`/`|**Root** — starting point of the entire file system|
|`/home`|Users' personal files|
|`/root`|Home directory of the root user|
|`/etc`|System and application **configuration files**|
|`/var`|Frequently changing data such as **logs, cache, databases**|
|`/tmp`|Temporary files|
|`/usr`|Most user applications, libraries and utilities|
|`/bin`|Essential user commands/programs|
|`/sbin`|Essential system/admin commands|
|`/dev`|Represents hardware/devices|
|`/proc`|Information about **running processes and kernel**|
|`/sys`|Information about hardware and kernel|
|`/boot`|Files needed to **boot Linux**|
|`/opt`|Optional/third-party software|
|`/mnt`|Temporary mount points|
|`/media`|Mounted removable devices such as USB drives|

```
/
├── home/
│   └── user/
├── etc/
├── var/
│   └── log/
├── tmp/
├── usr/
├── bin/
├── dev/
├── proc/
├── sys/
└── boot/
```

## Linux File Permission

Linux permissions control **who can access a file or directory and what they can do with it**.

|Permission|Symbol|For a File|For a Directory|
|---|---|---|---|
|**Read**|`r`|View file contents|List files inside|
|**Write**|`w`|Modify file contents|Create, delete, or rename files|
|**Execute**|`x`|Run the file as a program|Enter/access the directory|

**Important:** To delete a file, you generally need **write + execute permission on the parent directory**, not necessarily write permission on the file itself.

### Permissions apply to 3 groups

- **Owner (User)** → Person who owns the file.
- **Group** → Users belonging to the file's group.
- **Others** → Everyone else.

**Example:**

```
-rwxr-xr--
```

**Breakdown:**

```
Owner   → rwx

Group   → r-x

Others  → r--
```

So:

- Owner → **read + write + execute**
- Group → **read + execute**
- Others → **read only**

When you run:

```
ls -l
```

you may see:

```
-rwxr-xr--
```

Break it into **4 parts**:

```
- | rwx | r-x | r--

  |     |     |

  |     |     └── Others

  |     └──────── Group

  └────────────── Owner
```

- **`-`** → Regular file
    - `d` = directory
    - `l` = symbolic link
- **`rwx` (Owner)** → Owner can **Read + Write + Execute**
- **`r-x` (Group)** → Group can **Read + Execute**
- **`r--` (Others)** → Others can **Read only**

### Permission symbols

- `r` = **Read**
- `w` = **Write**
- `x` = **Execute**
- `-` = **Permission not given**

### Numeric (Octal) Notation

Linux permissions can also be written using **numbers instead of** `rwx`.

|Permission|Value|
|---|--:|
|`r` (Read)|**4**|
|`w` (Write)|**2**|
|`x` (Execute)|**1**|
|`-` (None)|**0**|

For each group (**Owner, Group, Others**), add the values:

- `rwx` → 4 + 2 + 1 = **7**
- `rw-` → 4 + 2 = **6**
- `r-x` → 4 + 1 = **5**
- `r--` → 4 = **4**
- `-wx` → 2 + 1 = **3**
- `-w-` → 2 = **2**
- `--x` → 1 = **1**
- `---` → **0**

## Linux Logs

**Linux logs** are records of activities and events that happen on a Linux system. They are mainly used for **troubleshooting, monitoring, and security investigation**.

| Log / Location             | What it records                                                             |
| -------------------------- | --------------------------------------------------------------------------- |
| `/var/log/auth.log`        | User **login, SSH, sudo, authentication** events — Debian/Ubuntu            |
| `/var/log/secure`          | Authentication and security events — RHEL (Red Hat Enterprise Linux)/CentOS |
| `/var/log/syslog`          | General **system activity** — Debian/Ubuntu                                 |
| `/var/log/messages`        | General system messages — RHEL-based systems                                |
| `/var/log/kern.log`        | **Kernel** messages                                                         |
| `/var/log/boot.log`        | **System boot** messages                                                    |
| `/var/log/dpkg.log`        | Package installation/removal — Debian/Ubuntu                                |
| `/var/log/apt/`            | APT package-manager activity                                                |
| `/var/log/audit/audit.log` | Detailed **security/audit events** when `auditd` is enabled                 |