
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

# Bind Shell 
# Reverse shell 
