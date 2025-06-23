# SSH & Socks Method
For example we have an open SSH port and a closed mysql port 
```shell-session
PORT     STATE  SERVICE
22/tcp   open   ssh
3306/tcp closed mysql
```
We can either
1. ssh into the server and access MySQL on the server
2. Port forward it and access it locally

Port to localhost on port 1234
```shell-session
ssh -L 1234:localhost:3306 username@10.129.202.64
```
This tells the ssh client to request the SSH server to forward all data we sent via the port 1234 to localhost:3306 on the compromised server. 

## Confirm it works
```
netstat -antp | grep 1234
nmap -v -sV -p1234 localhost
```

## Multiple Port Forwarding
```shell-session
ssh -L 1234:localhost:3306 -L 8080:localhost:80 ubuntu@10.129.202.64
```

# DNS Tunneling
Instead of using HTTPS or HTTP to send data between two hosts, we can also use DNS. 

send data inside TXT records through encrypted Command & Control channel 

go for evading firewall detections which strip  the HTTPS connections and sniff the traffic. 
[Dnscat2](5%20Lateral%20Movement/Pivoting/Tools/Dnscat2.md)

# ICMP Tunneling
doesn't work on their computer yet again 
```
pilorekenorse@htb[/htb]$ sudo apt install automake autoconf -y
pilorekenorse@htb[/htb]$ cd ptunnel-ng/
pilorekenorse@htb[/htb]$ sed -i '$s/.*/LDFLAGS=-static "${NEW_WD}\/configure" --enable-static $@ \&\& make clean \&\& make -j${BUILDJOBS:-4} all/' autogen.sh
pilorekenorse@htb[/htb]$ ./autogen.sh
```
copy the whole folder to pivot host


go to ptunnel-ng/src 
then run 

```shell-session
sudo ./ptunnel-ng -r10.129.202.64 -R22
```

from attack host
```shell-session
sudo ./ptunnel-ng -p10.129.202.64 -l2222 -r10.129.202.64 -R22
```

```
ssh -p2222 -lubuntu 127.0.0.1
```

## enabling dynamic port forwarding over SSH on top of 
```
ssh -D 9050 -p2222 -lubuntu 127.0.0.1
```

then you can use proxychains