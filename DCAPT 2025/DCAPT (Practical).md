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
