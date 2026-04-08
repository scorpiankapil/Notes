### ~(tilde)
It shows the Home Directory of current user.

### / (slash) 
It is the the root directory in Linux and all folders starts from / here.

### /bin (binary) 
It stores the binary files of basic commands that Linux needs to work like ls, cp, mv, rm etc.

### /boot 
It contains files that are needed to start (boot) the Linux system, it also contains the bootloader files (like GRUB) and Linux kernal is stored in this directory.
Without /boot, linux cannot start.
- `vmlinuz` → Linux kernel file
- `initrd` / `initramfs` → temporary file system used during boot
- `grub/` → bootloader configuration files

**Bootloader** files in Linux are stored in the `/boot` directory and are used to load the kernel and start the operating system.

### /dev 
dev stands for device. It contains special files that represent hardware devices. Linux treats hardware devices as files, and those files are stored in /dev.
These files allow the operating system to communicate with hardware like disks, keyboards, and USB devices.
Most device files in /dev are created automatically at system boot.
`/dev` directory in Linux contains device files that represent hardware devices and allow the OS to interact with them.

### /etc 
It stores system configuration files.
It contains settings for operating system, and installed software.
User accounts, groups, and network settings are defined here.
Most files in `/etc` can be modified only by the root (administrator).
Linux reads `/etc` files during system startup.

### /home directory
**`/home`** contains **home directories of normal users**.
Each user gets a **separate folder** inside `/home`.
It contains user files like **Documents, Downloads, Desktop, Music, Videos**.
Users have **full permission** to read, write, and delete their own files here.
Files in `/home` are **not required for OS working** (only user work).

### /lib
- /lib stands for library
- **`/lib`** directory stores library files required to run applications and system commands.
- Programs in **`/bin` and `/sbin`** depend on the libraries stored in `/lib`.
- These libraries provide **common functions** used by many programs.
- `/lib` libraries are required **during system boot**.
- Without `/lib`, the Linux system cannot work properly.

#### /lib32 and /lib64
`lib32` and `lib64` directories store 32-bit and 64-bit libraries respectively to support different types of applications in Linux.

### /lost+found
- /lost+found directory is used to store recovered files.
- It is automatically created when a Linux filesystem is made.
- It is mainly used by the filesystem check tool (fsck).
- After a system crash or improper shutdown, fsck puts recovered data here.
- Files inside /lost+found usually have numeric names instead of original names.
- Normal users do not work with this directory; it is meant for system recovery.

### /media
- **`/media`** directory is used to mount removable storage devices.
- Devices like USB drives, external hard disks, CDs/DVDs are attached here.
- Linux automatically creates folders inside `/media` when a device is connected.
- Each mounted device gets its **own directory** under `/media`.
- Users can access files of the device through these folders.
- When the device is removed, the folder inside `/media` is automatically removed.

### /mnt
- **`/mnt`** directory is used as a **temporary mount point** in Linux.
- It is mainly used by **system administrators**.
- **Mount** means **connecting a storage device or filesystem** to the Linux directory tree so it can be accessed.
- We use **mounting** to **read and write data** from disks, USB drives, or network storage.
- Devices are **manually mounted** in `/mnt` using the `mount` command.
- `/mnt` is commonly used for **testing, recovery, and maintenance tasks**.
- Unlike `/media`, devices are **not auto-mounted** here.

### /opt
- **`/opt`** stands for **optional**.
- It is used to store **third-party or optional software**.
- Software in `/opt` is **not part of the core Linux system**.
- Each application usually has **its own separate folder** inside `/opt`.
- This keeps optional software **organized and isolated** from system files.
- Commonly used for **large applications** like Google Chrome, Oracle, or custom software.

### /proc
- /proc is a virtual directory (it does not exist on the disk).
- It is created and managed by the Linux kernel.
- It provides real-time information about the system.
- It contains details about CPU, memory, and hardware status.
- Each running process has a folder in /proc using its process ID (PID).
- /proc is mainly used for system monitoring and troubleshooting.

### /root 
- **`/root`** is the home directory of the root user in Linux.
- The **root user** is the system administrator with full privileges.
- `/root` stores root user’s personal files and configuration.
- Normal users cannot access `/root` without special permission.
- `/root` is separate from `/home`, which is for normal users.
- This separation improves system security.

### /sbin
- **`/sbin`** stands for **system binaries**.
- It contains **important system administration commands**.
- These commands are mainly used by only the **root (administrator)** user.
- Programs in `/sbin` are needed for **system booting and recovery**.
- Normal users usually **do not have permission** to run `/sbin` commands.
- Examples of `/sbin` commands include **`fsck`**, **`ifconfig`**, **`reboot`**, and **`shutdown`**

### /bin
- **`/bin`** stands for **binary**.
- It contains **essential command programs** needed by the system.
- Commands in `/bin` are used by **both normal users and the root user**.
- These commands are required for **basic system operation**.
- `/bin` is needed even when the system is in **single-user or recovery mode**.
- Examples of `/bin` commands include **`ls`**, **`cp`**, **`mv`**, **`rm`**, and **`cat`**.

### /srv 
- **`/srv`** stands for **service**.
- It is used to store **data related to system services**.
- Services like **web servers, FTP servers, or file servers** keep their data here.
- The data in `/srv` is meant to be **accessed by users or clients**.
- It helps **separate service data** from system and user data.
- Use of `/srv` follows the **Linux Filesystem Hierarchy Standard (FHS)**.

### /sys
- **`/sys`** is a **virtual directory** created by the Linux kernel.
- It provides **real-time information about hardware and devices**.
- Data in `/sys` is organized in a **tree structure**.
- It allows users and programs to **view and change kernel parameters**.
- `/sys` is mainly used for **hardware management and configuration**.
- Data in `/sys` is **updated in real time**.
- Files in `/sys` are **not stored on disk** and exist only while the system is running.

### /tmp
- **`/tmp`** stands for temporary.
- It is used to store temporary files created by the system and applications.
- Files in `/tmp` are used for short-term processing.
- Data stored in `/tmp` is not permanent and may be deleted automatically.
- `/tmp` is usually cleared when the system reboots.
- All users can read and write files in `/tmp`.
- `/tmp` has the Sticky Bit enabled, which means only the user who created a file can delete it.
- Root (administrator) is an exception and can delete any file in `/tmp`; this rule exists for security.

### /usr
- **`/usr`** stands for **Unix System Resources**.
- It contains **user-level programs and applications**.
- Most software installed on the system is stored inside `/usr`.
- **`/usr/bin`** holds user commands and executable files.
- **`/usr/lib`** contains libraries needed by programs in `/usr/bin`.
- Files in `/usr` are **not required during system boot**.

## File & Directory Commands
- **`ls`** → Lists files and folders in the current directory
    - **`-a`** → shows **all files**, including **hidden files** (those starting with `.`).
    - **`-l`** → shows **detailed information** (permissions, owner, group, size, date).
- **`pwd`** → Shows the present (current) working directory
- **`cd`** → Changes directory
    - Example: `cd /home/user`   
- **`cd /`** → Changes the current directory to the **root directory** (`/`).
- **`cd ~`** → Changes the current directory to the **home directory** of the user.
- **`cd -`** → Switches back to the **previous directory** you were working in.
- **`mkdir`** → Creates a new directory
    - `mkdir -p` creates a directory along with its parent directories if they do not already exist.
- **`rmdir`** → Deletes an empty directory

#### Absolute Path
- An **absolute path** gives the **full location** of a file/folder.
- It **always starts with `/` (root)**.
- It works **from anywhere** in the system.
- Example: `/home/kapil/Documents/file.txt`

#### Relative Path
- A **relative path** gives the location **from the current directory**.
- It **does not start with `/`**.
- It depends on **where you are right now**.
- Example: `Documents/file.txt` (when you are in `/home/kapil`)

## File Handling Commands
- **`touch`** → Creates an empty file
- **`cat`** → Displays file content
- **`cp`** → Copies files or directories
- **`mv`** → Moves or renames files/directories
- **`rm`** → Deletes files or directories
- **`rm -rf`** forcefully and recursively deletes files and directories without asking for confirmation in Linux.

## Help & Utility Commands
- **`man`** → Shows manual/help of a command
    - Example: `man ls`    
- **`history`** → Shows previously used commands
- **`echo`** → Prints text on terminal

