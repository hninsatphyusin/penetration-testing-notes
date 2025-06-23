
If your pivot is a windows machine
need administrator access 
```cmd-session
netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=<external facing ip addr of pivot> connectport=3389 connectaddress=<internal ip addr of target>
```


```
netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=10.129.176.76 connectport=3389 connectaddress=172.16.6.50
```
to check: 
```
netsh.exe interface portproxy show v4tov4
```

to do stuff now
```
xfreerdp3 /v:<external facing ip addr of pivot>:8080 /u:victor /p:pass@123
```