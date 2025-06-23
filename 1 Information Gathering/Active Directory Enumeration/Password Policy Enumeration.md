using [[Crackmapexec]] or rpcclient 

```
rpcclient -U "" -N 172.16.5.5

querydominfo
```

```
enum4linux -P 172.16.5.5
enum4linux-ng -P 10.10.10.161 -oA ilfreight
cat ilfreight.json
```

Null Sessions 
```
net use \\DC01\ipc$ "" /u:""

net use \\DC01\ipc$ "password" /u:guest
```

LDAPSearch
```
ldapsearch -H 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

on Windows 
```
C: net accounts
PS: 
import-module .\PowerView.ps1
Get-DomainPolicy
```

