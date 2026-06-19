# Proxychains

**ProxyChains** is a Linux tool that forces network traffic from other applications to pass through one or more proxy servers.

ProxyChains allows you to route the traffic of a program (such as Nmap, SSH, Firefox, or Metasploit) through a proxy server.

### Real Pivoting Example

Suppose:

```
Your Machine:      192.168.1.100Victim Machine:    192.168.1.50Internal Server:   10.10.10.5
```

You can reach:

```
192.168.1.50
```

But you **cannot** reach:

```
10.10.10.5
```

because it's inside the victim's internal network.

After compromising `192.168.1.50`, you create a SOCKS proxy on it.

Now:

```
proxychains nmap 10.10.10.5
```

actually becomes:

```
Your PC   │   ▼Victim (SOCKS Proxy)   │   ▼10.10.10.5
```

The scan works because the victim machine can access the internal server.