# Filtered Ports 
Firewalls have certain rules to handle connections
packets can either be dropped or rejected 


How to see whether packets are droppped
```shell-session
pilorekenorse@htb[/htb]$ sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 15:45 CEST
SENT (0.0381s) TCP 10.10.14.2:60277 > 10.129.2.28:139 S ttl=47 id=14523 iplen=44  seq=4175236769 win=1024 <mss 1460>
SENT (1.0411s) TCP 10.10.14.2:60278 > 10.129.2.28:139 S ttl=45 id=7372 iplen=44  seq=4175171232 win=1024 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up.

PORT    STATE    SERVICE
139/tcp filtered netbios-ssn
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)

Nmap done: 1 IP address (1 host up) scanned in 2.06 seconds
```
The time taken is much longer than average and sent packages but no receive

How to see whether packets are rejected
```shell-session
sudo nmap 10.129.2.28 -p 445 --packet-trace -n --disable-arp-ping -Pn

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 15:55 CEST
SENT (0.0388s) TCP 10.129.2.28:52472 > 10.129.2.28:445 S ttl=49 id=21763 iplen=44  seq=1418633433 win=1024 <mss 1460>
RCVD (0.0487s) ICMP [10.129.2.28 > 10.129.2.28 Port 445 unreachable (type=3/code=3) ] IP [ttl=64 id=20998 iplen=72 ]
Nmap scan report for 10.129.2.28
Host is up (0.0099s latency).

PORT    STATE    SERVICE
445/tcp filtered microsoft-ds
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)

Nmap done: 1 IP address (1 host up) scanned in 0.05 seconds
```

SENT packet, RVCD packet that says port is unreachable 


# Open UDP Ports 
key flag: -sU
```shell-session
sudo nmap 10.129.2.28 -F -sU
```
does not require 3-way handshake, no acknowledgment received. Timeout is much longer, UDP scans much slower than TCP scans (-sS), we only get response if the application is configured to do so. 

```shell-session
sudo nmap 10.129.2.28 -sU -Pn -n --disable-arp-ping --packet-trace -p 100 --reason 
```
but we get ICMP response of error code 3 (port unreachable) is the port is closed

If nothing is received, then is open | filtered. 

# Bypassing Firewall and IDS/IPS 

ACK scan (-sA)
```shell-session
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```

Decoys (-D)
```shell-session
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```
-D RND:5	Generates five random IP addresses that indicates the source IP the connection comes from.
The spoofed packets are often filtered out by ISPs and routers, even though they come from the same network range.

# Specifying a IP address to spoof (-S)
```shell-session
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```

# DNS Proxy 
use tcp port 53 instead of the usual udp port 53
```shell-session
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```
