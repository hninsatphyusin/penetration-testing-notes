
# Basic syntax
```shell-session
nmap <scan types> <options> <target>
```

```shell-session
<SNIP>
SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sN/sF/sX: TCP Null, FIN, and Xmas scans
  --scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
<SNIP>
```
By default, TCP-SYN scan (-sS) is used 
sends one packet with SYN flag, does not complete the 3-way handshake, does not establish a full TCP connection to the scanned port 

```
- If our target sends a `SYN-ACK` flagged packet back to us, Nmap detects that the port is `open`.
- If the target responds with an `RST` flagged packet, it is an indicator that the port is `closed`.
- If Nmap does not receive a packet back, it will display it as `filtered`. Depending on the firewall configuration, certain packets may be dropped or ignored by the firewall.
```


Types of Connection

| Flag | Property                       | Usage                                                                 |
| ---- | ------------------------------ | --------------------------------------------------------------------- |
| -sT  | TCP Connect()                  |                                                                       |
| -sA  | TCP ACK - sends the ACK packet |                                                                       |
| -sS  | TCP SYN Stealth                |                                                                       |
| -sU  | UDP Scan                       | Can be used to bypass firewall if firewall only block TCP connections |

# Performance Optimisation 
## Timeout 
default timeout is 100ms
```shell-session
sudo nmap 10.129.2.0/24 -F --initial-rtt-timeout 50ms --max-rtt-timeout 100ms
```

# Max Retries 
```shell-session
sudo nmap 10.129.2.0/24 -F --max-retries 0 
```
This may result in overlooking important information, default retries is 100

## Rates of packets sent
Useful if we know the network bandwidth, we can increase the min rate
```shell-session
sudo nmap 10.129.2.0/24 -F -oN tnet.minrate300 --min-rate 300
```

# Timing 
- T <0-5> determine the aggressiveness of scan 
- `-T 0` / `-T paranoid`
- `-T 1` / `-T sneaky`
- `-T 2` / `-T polite`
- `-T 3` / `-T normal`
- `-T 4` / `-T aggressive`
- `-T 5` / `-T insane`
default is normal obv 

# Sudo 
sudo -> TCP Connect() scan (-sT) is performed instead of TCP SYN (-sS) scan. Have to manually add the -sS flag

With Sudo and Without Sudo 

| Feature/Capability       | With `sudo`/Root                 | Without `sudo`                                                 |
| ------------------------ | -------------------------------- | -------------------------------------------------------------- |
| **TCP SYN Scan (`-sS`)** | Supported                        | Not supported (defaults to TCP Connect Scan `-sT`).            |
| **UDP Scan (`-sU`)**     | Supported                        | Not supported (Nmap may not send proper UDP packets).          |
| **OS Detection (`-O`)**  | Supported                        | Partially supported (less reliable without raw packet access). |
| **Ping Sweep (`-sn`)**   | ICMP and ARP requests supported  | Limited to TCP/UDP-based pings.                                |
| **Packet Crafting**      | Fully supported                  | Limited (requires raw socket access).                          |
| **Performance**          | More efficient, uses raw sockets | Less efficient, relies on system-level APIs.                   |
