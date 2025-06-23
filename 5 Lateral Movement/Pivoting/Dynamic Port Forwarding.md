In the case of pivoting, where the target host is the pivot to another network, and we can to scan that network. 
To do so we start a SOCKS listener on localhost and then configure SSH to forward that traffic via SSH into the network after connecting to the target host 

Can be used to bypass firewall
## Socks Proxy / SSH Tunnelling
```shell-session
ssh -D 9050 username@10.129.202.64
```
configure proxy chain
```shell-session
tail -4 /etc/proxychains.conf

//set 
socks4 127.0.0.1 9050
```
use proxy chains
```
proxychains nmap -v -sn 172.16.5.1-200
```
can only perform a full TCP connect scan over proxychains because it cannot understand partial packets 
## scan individual host
```
proxychains nmap -v -Pn -sT 172.16.5.19
```

## Use metasploit with proxychains
```
proxychains msfconsole
```
## Use xfreerdp with Proxychains
```
proxychains xfreerdp3 /v: /u: /p:
```

# Chisel 
written in Go that uses HTTP to transport data that is secured using SSH

Download an older version of chisel to copy to HTB host, attack host just sudo apt install chisel
```
wget https://github.com/jpillora/chisel/releases/download/v1.7.7/chisel_1.7.7_linux_amd64.gz
```

copy to pivot host
```
scp chisel ubuntu@10.129.202.64:~/
```
run on pivot host
```
./chisel server -v -p 1234 --socks5
```

connect to pivot 
```
./chisel client -v 10.129.202.64:1234 socks
```

check proxy chain if there is port 1080
```
tail -f /etc/proxychains.conf 

#
#       proxy types: http, socks4, socks5
#        ( auth types supported: "basic"-http  "user/pass"-socks )
#
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
# socks4 	127.0.0.1 9050
socks5 127.0.0.1 1080
```

then u can just proxychain commands 

