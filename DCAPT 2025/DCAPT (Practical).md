```
ssh -o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedAlgorithms=+ssh-rsa user@172.20.10.5
```

An SSH command used to connect to a remote machine that only supports old RSA SSH security methods.
- `ssh` → starts a secure remote connection
- `-o` → sets SSH options
- `HostKeyAlgorithms=+ssh-rsa` → allows old RSA host keys
- `PubkeyAcceptedAlgorithms=+ssh-rsa` → allows old RSA authentication
- `user@172.20.10.5` → connects as user `user` to IP `172.20.10.5`

Used when connecting to old servers or devices that do not support modern SSH algorithms.

`ssh-rsa` is outdated and less secure, so this is mainly for compatibility with legacy systems.

---

# Nikto

- Open-source web server vulnerability scanner used in cybersecurity and penetration testing.
- Performs active scanning on web servers and web applications.
- Detects outdated server software such as Apache, Nginx, IIS, and Tomcat.
- Identifies dangerous files, default pages, backup files, and exposed directories.
- Finds server misconfigurations and weak SSL/TLS settings.
- Helps discover known web server vulnerabilities and security weaknesses.
- Commonly used during reconnaissance and initial security assessment phases.
- Generates reports in formats like HTML, TXT, CSV, and XML.
- Easy to install and use on Linux systems like Kali Linux.
- Can trigger IDS, IPS, and WAF systems because scans are noisy and easily detectable.
- Frequently used along with tools like Nmap, Burp Suite, and [Nuclei](https://github.com/projectdiscovery/nuclei?utm_source=chatgpt.com).
- Useful for CTFs, labs, vulnerability assessments, and authorized penetration testing.

# Naabu

- Fast open-source port scanning tool developed by ProjectDiscovery.
- Used for fast network reconnaissance and port discovery in cybersecurity.
- Detects open ports on target systems very quickly.
- Commonly used in bug bounty hunting and penetration testing.
- Supports scanning single IPs, multiple hosts, CIDR ranges, and domains.
- Can perform SYN scans and CONNECT scans.
- Lightweight and faster than traditional scanners in many cases.
- Integrates easily with other ProjectDiscovery tools like:
    - [Nuclei](https://github.com/projectdiscovery/nuclei?utm_source=chatgpt.com)
    - [Subfinder](https://github.com/projectdiscovery/subfinder?utm_source=chatgpt.com)
    - [httpx](https://github.com/projectdiscovery/httpx?utm_source=chatgpt.com)
- Often combined with Nmap for deeper service/version detection.
- Supports rate limiting for controlled scanning.
- Can scan thousands of ports rapidly using asynchronous techniques.
- Useful for attack surface mapping and initial enumeration.
- Works well in automation pipelines and recon scripts.
- Commonly used by professional pentesters and red teamers.
- Supports output saving in different formats for later analysis.

# Medusa 

- Fast and parallel login brute-forcing tool used in penetration testing.
- Used to test authentication security of different network services.
- Supports multiple protocols such as SSH, FTP, HTTP, SMB, RDP, MySQL, and Telnet.
- Commonly used by cybersecurity professionals for password auditing and credential testing.
- Supports single username, multiple usernames, single password, and password lists.
- Can perform multi-threaded attacks for faster testing.
- Useful in CTFs, labs, and authorized security assessments.
- Supports verbose output and result reporting.
- Works on Linux systems including Kali Linux.
```
 medusa -h 192.168.1.10 -u root -P rockyou.txt -M ssh
```

# John the Ripper

- Password cracking and password auditing tool used in Kali Linux.
- Works by taking a password hash and trying different password guesses.
- Converts guessed passwords into hashes and compares them with the target hash.
- If the generated hash matches the target hash, the password is cracked.
- Supports multiple attack methods like dictionary attack, brute-force attack, and hybrid attack.
- Supports many hash types such as MD5, SHA1, SHA256, NTLM, ZIP/RAR, and Linux shadow hashes.
```
sudo john -format=crypt --wordlist=pass.txt hash.txt
```


# Hashcat

- Advanced password cracking and recovery tool used in Kali Linux.
- Uses GPU acceleration, making it much faster than many traditional cracking tools.
- Works by taking a password hash and generating password guesses to find the correct password.
- Converts guessed passwords into hashes and compares them with the target hash.
- Supports attack modes like dictionary attack, brute-force attack, mask attack, and hybrid attack.
- Supports many hash types such as MD5, SHA1, SHA256, NTLM, WPA/WPA2, ZIP/RAR, and Linux hashes
```
hashcat -m 0 hash.txt rockyou.txt
```

# FFUF

- Fast web fuzzing and directory discovery tool used in Kali Linux.
- Used to find hidden directories, files, subdomains, parameters, and APIs.
- Works by sending multiple requests with different payloads from a wordlist.
- Replaces the keyword FUZZ in the URL or request with words from the wordlist.
- Commonly used for web application reconnaissance and vulnerability testing.
- Supports directory fuzzing, virtual host fuzzing, parameter fuzzing, and POST request fuzzing.
- Very fast and lightweight compared to many other fuzzing tools.
```
ffuf -u http://target.com/FUZZ -w wordlist.txt
```

# Dirsearch

- Web path and directory brute-forcing tool used in Kali Linux.
- Used to discover hidden files, directories, admin panels, and backup files on websites.
- Works by sending HTTP requests using words from a wordlist.
- Compares server responses to identify valid paths and resources.
- Commonly used in web reconnaissance and penetration testing.
- Supports recursive scanning, extensions scanning, threads, proxies, and authentication.
- Can detect files like `.php`, `.html`, `.bak`, `.zip`, and hidden admin pages.
```
dirsearch -u http://172.20.10.2/
```

# Telnet

1. Used for remote communication between computers.
2. Works on port 23 by default.
3. Sends data in plain text (not secure).
4. Mainly used for testing ports and old network devices.
5. Does not provide encryption or secure authentication.
6. Mostly replaced by SSH in modern systems.

# SSH (Secure Shell)

1. Used for secure remote login and administration.
2. Works on port 22 by default.
3. Encrypts all communication between client and server.
4. Supports password and key-based authentication.
5. Commonly used by system administrators and developers.
6. Can securely transfer files using SCP/SFTP.

