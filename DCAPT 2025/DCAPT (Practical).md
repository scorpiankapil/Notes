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
