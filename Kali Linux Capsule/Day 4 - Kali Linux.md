# Process
- A **process** is a **program that is currently running**.
- When a program is executed, the operating system **creates a process** for it.
- Each process has a **unique Process ID (PID)**.
- A process uses **CPU, memory, files, and other system resources**.
- Processes are **created, managed, and terminated by the kernel**.
- During execution, a process **loads required libraries**.
- It **opens files, devices, and memory areas** to perform tasks.
- The process holds **open file descriptors** for these resources.
- As long as the process is running, these resources remain **open**.
- When the process **terminates**, the kernel **closes all open files and releases resources**.

## How File Descriptors Manage Files in Linux
In **Linux**, **file descriptors (FDs)** are used to **manage how processes access files and I/O resources**.

- When a **process opens a file**, the **kernel assigns a file descriptor** (a small number like 3, 4, 5…).
- The kernel creates an **entry in the global file table** that stores file details (mode, offset, permissions).
- The file descriptor **acts as a handle** that links the process to that file entry.
- Whenever the process **reads or writes**, it uses the **file descriptor**, not the filename.
- The kernel uses the FD to **locate the file**, check **permissions**, and perform **I/O operations**.
- When the process **closes the file or exits**, the kernel **removes the FD** and frees resources.


### File Descriptor Table
- Every **process has its own file descriptor table**.
- It is updated by Linux Kernal only.
- The table stores **file descriptor numbers** (0, 1, 2, 3, …).
- Each file descriptor **points to an entry in the global file table**.
- It helps the kernel know **which file a process is using**.
- Without this table, the kernel cannot manage process I/O properly.

### Global File Table
- The **Global File Table** is a **list maintained by the kernel**.
- It keeps information about **all open files** in the system.
- Whenever any program opens a file, the kernel **adds an entry** to this table.
- Many processes can **use the same file**, so they may **point to the same table entry**.
- The table stores details like **read/write mode** and **current position in the file**.
- When all programs close a file, the kernel **removes that entry**.

### Inode Table
The inode table stores metadata of files and helps the kernel locate file data on disk.

- The **inode table** is a **kernel-managed list** that stores **information about files**.
- An **inode** does **not store the file name**; it stores file **metadata**.
- Each file has a **unique inode number**.
- The inode stores details like **file size, owner, permissions, timestamps**.
- It also stores **where the file’s data is located on disk** (data blocks).
- When a file is opened, the kernel uses the inode to **access the actual file data**.

### How it works
In Linux, when a program opens a file, the kernel gives it a **file descriptor**, which is just a number used by the process. This file descriptor points to an entry in the **global file table**, which stores how the file is being used, such as read or write mode and the current position in the file. The global file table entry then points to the **inode table**, which contains the actual information about the file, like its permissions, size, and where the file is stored on the disk. Using this chain, the kernel can safely and efficiently access file meta data for the process.

# Commands

##### Head command
The head command in Linux displays the first few lines of a file, by default the first 10 lines.
```
head file.txt
```
```
head -n 5 file.txt
```

##### Less command
Used to **read a file slowly**, you can scroll **up and down**.
```
less file.txt
```

##### More command
Used to **read a file page by page**, but only **forward**.
```
more file.txt
```

##### Tail command
Used to **see the last part of a file** (last 10 lines).
```
tail file.txt
```

##### wc(word count) command
It is used to **count lines, words, and characters** in a file or input
```
wc file.txt
wc -l file.txt   # count lines
wc -w file.txt   # count words
wc -c file.txt   # count characters

```

##### Tac command
`tac` command displays the contents of a file in reverse line order.
```
tac file.txt

```

##### Sed command 
`sed` is a stream editor used to search, replace, and modify text in files or input.

```
sed -n '1p' /etc/passwd
sed -n '1p;5p' /etc/passwd

```