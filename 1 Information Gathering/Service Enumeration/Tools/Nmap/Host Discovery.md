# Scan subnet 
```shell-session
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
``` 

|**Scanning Options**|**Description**|
|---|---|
|`10.129.2.0/24`|Target network range.|
|`-sn`|Disables port scanning.|
|`-oA tnet`|Stores the results in all formats starting with the name 'tnet'.|

# Scan Single IP 
```shell-session
sudo nmap 10.129.2.18 -sn -oA host 
```
![[Screenshot 2024-12-29 at 2.17.34 PM.png]]
When port scanning is disabled, the scan is done with ICMP echo request (-PE)
But ARP scan is done faster and then it already is able to find out whether the host is alive or not 

To disable ARP pings
```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping
```

Identify host OS by the TTL of ICMP Echo reply from scanned machine 
```shell-session
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:12 CEST
SENT (0.0107s) ICMP [10.10.14.2 > 10.129.2.18 Echo request (type=8/code=0) id=13607 seq=0] IP [ttl=255 id=23541 iplen=28 ]
RCVD (0.0152s) ICMP [10.129.2.18 > 10.10.14.2 Echo reply (type=0/code=0) id=13607 seq=0] IP [ttl=128 id=40622 iplen=28 ]
Nmap scan report for 10.129.2.18
Host is up (0.086s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```
Here the TTL is 128 so its Windows
Linux/Unix is 64
Networking devices (like routers) is 255

# ARP VS ICMP 

-sN: ARP ping - ARP reply
ARP - Address Resolution Protocol: Finds the MAC address of the host - Link Layer (layer 2)

ICMP - Internet Control Message Protocl (Network Layer): Used to check the reachability of a host and measure the round-trip time for messages to reach the host and return 

### **Key Differences**

|Feature|ARP Ping|ICMP Echo Request|
|---|---|---|
|**Protocol**|ARP|ICMP|
|**Layer**|Data Link Layer (Layer 2)|Network Layer (Layer 3)|
|**Scope**|Local subnet only|Local and remote networks|
|**Firewall Impact**|Unaffected (essential for LAN)|May be blocked by firewalls|
|**Purpose**|Resolves MAC addresses|Checks host reachability|
|**Packet Type**|ARP Request/Reply|Echo Request/Reply|
