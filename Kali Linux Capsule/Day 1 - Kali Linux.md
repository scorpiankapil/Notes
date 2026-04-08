# History of Linux
At 1964 -> At Bell Laboratory in New Jersey, this project was started and the purpose of this project was to create a OS so that multiple users can use one operating system at the same time.

At 1969 -> Withdraw this project 
But they (**Dennis Ritchie and Ken Thompson**) are not satisfied and restarted the project 
and they created the  UNIX Operating System.

In 1975, the new version of UNIX was released, UNIX v6
And at same time multiple companies created commercial versions using UNIX v6, called flavours of unix
- IBM - Aux
- Sunsystem - Sunsolaris
- MacOS
- HP - UX

In 1991, Linus Torvalds, a computer science student at the University of Helsinki, created Linux.
Linus Torvalds was using MINIX, a small Unix-like OS made for teaching by his teacher Andrew Stuart Tanenbaum. MINIX had license restriction and limited features.
But he wanted a free operating system with full control over the source code for better hardware support. So, Linux was created to be free, open-source, unix-like and multi-user & multitasking.

Between 1991 to 1995, there was a movement called Free Software Movement, the purpose of this movement

## UNIX Operating System
* UNIX is an operating system developed by Dennis Ritchie and Ken Thompson in 1969 at Bell Laboratories.
* It allows multiple users to use the same system at the same time.
* UNIX supports multitasking, meaning it can run many programs simultaneously.
* It is known for being stable, secure, and efficient.
* UNIX mainly uses a command-line interface.
* It has strong security features like users, groups, and file permissions.
* UNIX became the base for modern operating systems such as Linux and macOS.

## LINUX Operating System
* Linux is a free and open-source operating system kernel.
* It was created in 1991 by Linus Torvalds.
* Linux was designed as a Unix-like system.
* It supports multiple users using the same system at the same time.
* Linux supports multitasking, so many programs can run simultaneously.
* It is known for high security, stability, and performance.
* Linux is widely used in servers, cloud computing, cybersecurity, and supercomputers.
* Many operating systems called Linux distributions (like Ubuntu, Kali, Red Hat) are built using the Linux kernel.

### Features of Linux
- **Open Source** – Linux is free to use, modify, and distribute.
- **Multi-user** – Multiple users can use the same system at the same time.
- **Multitasking** – Can run many programs simultaneously without slowing down.
- **High Security** – Strong user, group, and file permission system.
- **Stability & Reliability** – Rarely crashes; can run for years without reboot.
- **Command Line & GUI Support** – Supports both **CLI** and **GUI** interfaces.
- **Portability** – Runs on different hardware platforms (PCs, servers, mobiles, IoT).
- **Networking Capabilities** – Built-in support for networking and servers.
- **Customizable** – Users can customize the kernel and desktop environment.
- **Wide Usage** – Used in servers, cloud computing, cybersecurity, supercomputers, and Android devices.

## GNU
- **GNU** is a **free software project** started in **1983**.
- It was founded by **Richard Stallman**.
- GNU stands for **“GNU’s Not Unix”**.
- The goal of GNU is to create a **completely free and open-source Unix-like operating system**.
- GNU provides essential system tools such as:
    - Compilers (GCC)
    - Shells (Bash)
    - Core utilities (ls, cp, mv, etc.)
- GNU follows the **GPL (General Public License)**, which allows users to use, modify, and share software freely.
- GNU did **not have its own kernel**, which is why it was later combined with the **Linux kernel** to form **GNU/Linux**.

**LINUX + GNU = OS**

## Operating System
* An Operating System (OS) is system software that controls the overall working of a computer.
* It acts as an interface between the user and the computer hardware.
* The OS manages hardware resources like CPU, memory, disk, and input/output devices.
* It allows users to run applications and programs.
* The OS supports multitasking, meaning multiple programs can run at the same time.
* It manages files and directories on storage devices.
* The OS provides security through user accounts, passwords, and permissions.
* Examples of operating systems include Windows, Linux, and macOS.

### Command-line Interface
* A Command Line Interface (CLI) is a way to interact with a computer by typing text commands instead of using a mouse.
* Users give instructions through a terminal or shell.
* Each command performs a specific task (like creating files, running programs, or managing systems).
* CLI is fast and powerful compared to graphical interfaces.
* It uses less system resources (memory and CPU).
* CLI is widely used in Unix and Linux systems.
* It is very important for system administration, programming, and cybersecurity.

### Graphical-user Interface
* A Graphical User Interface (GUI) allows users to interact with a computer using graphics instead of typing commands.
* It uses windows, icons, menus, and buttons (WIMP).
* Users can perform tasks using a mouse, touchpad, or touchscreen.
* GUI is easy to learn and user-friendly, especially for beginners.
* It allows visual interaction, like clicking, dragging, and scrolling.
* GUI requires more system resources than a command-line interface.
* GUI is commonly used in operating systems like Windows, Linux, and macOS.

## OS-Defined Data & User-Defined Data in Linux

### OS-Defined Data (Linux)
- OS-defined data is **automatically created by Linux** during **OS installation**.
- It is also created during **system booting** when the kernel loads system files.
- System configuration changes (users, network, services) generate OS-defined data.
- Installing or updating system software creates or modifies OS-defined files.
- It is stored in **system directories** like `/bin`, `/etc`, `/lib`, `/boot` and is **critical for OS functioning**.

### User-Defined Data (Linux)
- User-defined data is **created by users** while working on the system.
- It is created when users **save files, download data, or create programs**.
- User-installed applications can also create user-defined data.
- It is stored mainly in the **`/home/username/`** directory.
- User-defined data is **not essential for OS operation** and can be modified or deleted by the user.

## OS-Defined Data & User-Defined Data in Windows

### OS-Defined Data (Windows)
- OS-defined data is automatically created by the operating system during Windows installation.
- It is also created during **system boot** when Windows loads core system files and drivers.
- System configuration changes (users, registry settings, services) create or modify OS-defined data.
- Installing or updating system software and drivers generates OS-defined files.
- It is stored in **system folders** like `C:\Windows`, `C:\Program Files`, and `C:\Program Files (x86)` and is critical for Windows to run properly.

### User-Defined Data (Windows)
- User-defined data is created by users while using the system.
- It is created when users save documents, images, videos, or projects.
- Applications create user data when users download files or save settings.
- It is stored mainly in **user folders** like `C:\Users\Username\Documents`, `Downloads`, `Desktop`.
- User-defined data is not essential for OS operation and can be modified or deleted by the user.

## What is `/` (Slash) in Linux?
* / (slash) is called the root directory in Linux.
* It is the top-most directory of the Linux file system.
* All files and folders start from / in Linux.
* Directories like /home, /bin, /etc, /usr, /var are all inside /.
* Without /, the Linux file system cannot exist or work.

#### Default Directories in Linux
By default, a standard Linux installation typically includes around **19 main directories** under the **`/` (root) directory**. These directories organize the system files, user data, and application resources.
* [ / ] -: 19 Directories
    * Around 17 directories are operated by OS
    * Remaining 2 Directories
        * 1 is for Root User / Super User
        * And 1 is for Normal Users (Here another user can't see the data of another user)

**Examples include:**
- `/bin` for essential user binaries.
- `/etc` for configuration files.
- `/home` for user home directories.
- `/lib` for essential shared libraries.
- `/usr` for user applications and utilities.

These directories form the backbone of the Linux filesystem, helping the OS and users keep everything organized.

