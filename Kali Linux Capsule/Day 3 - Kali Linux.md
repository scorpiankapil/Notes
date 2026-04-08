## Input / Output Redirection
- **Input Redirection (`<`)**  
    Takes input **from a file** instead of the keyboard.
    - Example: `cat < file.txt`
        
- **Output Redirection (`>`)**  
    Sends output **to a file** (overwrites).
    - Example: `ls > list.txt`
        
- **Append Redirection (`>>`)**  
    Sends output **to a file without overwriting**.
    - Example: `echo hello >> notes.txt`
        
- **Error Redirection (`2>`)**  
    Sends **error messages** to a file.
    - Example: `ls wrongfile 2> error.txt`

## File Descriptors
A file descriptor is a number that Linux uses to identify where data comes from and where it goes.
Linux treats everything like a file — keyboard, screen, files, errors — and gives each one a number.

### Main File Descriptors

- **0 → STDIN (Input)**
    - **Default source:** Keyboard
    - **Location (device file):** `/dev/stdin`
    - Example:
        `cat 0< file.txt`
        
- **1 → STDOUT (Output)**
    - **Default destination:** Screen (Terminal)
    - **Location (device file):** `/dev/stdout`
    - Example:
        `ls 1> out.txt`
        
- **2 → STDERR (Error)**
    - **Default destination:** Screen (Terminal)
    - **Location (device file):** `/dev/stderr`
    - Example:
        `ls wrongfile 2> error.txt`

### What the Kernel Does for File Descriptors
When a program opens a file, the **kernel does these 3 main things**:

1️⃣ **Access Grant (Permission Check)**
- Kernel checks: _Is this user allowed to read/write this file?_
- If permission is denied → file descriptor is **not created**.

2️⃣ **Create Entry in Global File Table**
- Kernel creates an entry in its **global file table**.
- This entry stores:
    - File type
    - Access mode (read/write)
    - Current position (offset)

3️⃣ **Provide Location (Link FD to File)**
- Kernel assigns a file descriptor number (0, 1, 2, …).
- This FD points to the global file table entry, which points to the actual file location on disk.

## Commands

### Pipeline ( | )
A pipeline in Linux uses | to pass the output of one command as input to another command.
Example: `ls | wc -l`

### Tee
tee command displays command output on the screen and simultaneously writes it to a file.
