run Wireshark/TCPDump -> see ARP requests and replies, MDNS, and layer two packets 

```
sudo -E wireshark
sudo tcpdump -i ens224
```
for windows we can use `pktmon.exe`

## responder
tool built to listen, analyse, and poison LLMNBR, NBT-NS, and MDNS requests and responses 
```bash
sudo responder -I ens224 -A 
```

icmp sweep of subnet using fping 
```
fping -asgq 172.16.5.0/23
```

nmap scan 
hosts.txt contains results from responder fping etc. to see what common AD services r running on what device
```
sudo nmap -v -A -iL hosts.txt -oN /home/htb-student/Documents/host-enum
```
