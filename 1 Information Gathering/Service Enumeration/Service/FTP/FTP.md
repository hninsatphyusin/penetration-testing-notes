# Logging in as Anonymous
```shell-session
ftp 10.129.14.136 port_number (optional)
```
Use 'status', 'debug', 'trace' followed by 'ls' to get more information about the server 

```
ls -R 
tree
```

# Download all available files 
```shell-session
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136
```

# Using nmap to find more information about FTP 
```shell-session
sudo nmap --script-updatedb
```

```shell-session
find / -type f -name ftp* 2>/dev/null | grep scripts
```

```shell-session
sudo nmap -sV -p21 -sC -A 10.129.14.136
```
refer to [[nmap]] for explanation 

# Using nc/telnet to interact with FTP 

```shell-session
nc -nv 10.129.14.136 21
```

```shell-session
telnet 10.129.14.136 21
```

if FTP server runs with TLS/SSL encryption: 
```shell-session
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```



# Theory 
File Transfer Protocol 
Runs within the application layer of TCP/IP 
Port 21 (Control Channel), Port 20 (Data Transmission)

Link for FTP commands:  https://web.archive.org/web/20230326204635/https://www.smartfile.com/blog/the-ultimate-ftp-commands-list/

Link for FTP status codes: https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes

FTP is a clear-text protocol, can be sniffed if conditions on the network are right 
Possible that server offers anonymous FTP 

# Trivial File Transfer Protocol (TFTP)
- Simpler than FTP 
- Does not provide user authentication 
- uses UDP 
- may only be used in local and protected networks 
## Commands of TFTP:

| **Commands** | **Description**                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `connect`    | Sets the remote host, and optionally the port, for file transfers.                                                                     |
| `get`        | Transfers a file or set of files from the remote host to the local host.                                                               |
| `put`        | Transfers a file or set of files from the local host onto the remote host.                                                             |
| `quit`       | Exits tftp.                                                                                                                            |
| `status`     | Shows the current status of tftp, including the current transfer mode (ascii or binary), connection status, time-out value, and so on. |
| `verbose`    | Turns verbose mode, which displays additional information during file transfer, on or off.                                             |
