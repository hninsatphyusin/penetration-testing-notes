Network File System 
Same purpose as [[3 - Hacking/3.4 Services/SMB]], but uses different protocol 

Ports: 2049, 111

It does not have built-in mechanisms for authentication or authorization; instead, it relies on RPC's authentication options and file system-based authorization.

- **Authentication**: Typically uses **UNIX UID/GID** and group memberships.
- **Authorization**: Depends on the server's ability to map client user information into its file system's format and translate permissions into UNIX syntax.

However, mismatched UID/GID mappings between client and server can cause issues, and servers perform no additional checks. Due to these limitations, NFS with this authentication method is only secure in **trusted networks**.


# Footprinting

[[nmap]]
```shell-session
sudo nmap 10.129.135.203 -p111,2049 -sV -sC
```

```shell-session
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```
