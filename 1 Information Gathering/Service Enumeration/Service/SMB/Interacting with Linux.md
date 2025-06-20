# Smbclient 
```shell-session
smbclient -U "alex" //10.129.14.128/
```

anonymous login 
```
smbclient -N -L //10.129.236.209/
```

Going into a specific sharename 
```shell-session
smbclient //10.129.14.128/sharename 
```
after which, we can use the 'help' command to list all the possible commands we can execute 

Download files 
```
get filename.txt
```
smbclient also allows us to execute local system commands using an exclamation mark at the beginning "!command" without interrrupting the connection 

```
smbstatus
```
 information available here: samba version, who, which host, which share client is connected to. 

# Mounting the smb share 
do this when the file you want to import is too large to use get
```
sudo mkdir -p /mnt/sharename

sudo mount -t cifs -o username=username,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance
```


# RPCClient 
Remote Procedure Call - concept/tool to realize operational and work-sharing structures in networks and client-server architectures 

Alternatives for rpcclient: SMBmap, CrackMapExec, enum4linux-ng 

```
rpcclient -U'%' 10.129.14.128
```
supplying empty username and password by %

```shell-session
rpcclient -U "" 10.129.14.128
```

| **Query**                 | **Description**                                                    |
| ------------------------- | ------------------------------------------------------------------ |
| `srvinfo`                 | Server information.                                                |
| `enumdomains`             | Enumerate all domains that are deployed in the network.            |
| `querydominfo`            | Provides domain, server, and user information of deployed domains. |
| `netshareenumall`         | Enumerates all available shares.                                   |
| `netsharegetinfo <share>` | Provides information about a specific share.                       |
| `enumdomusers`            | Enumerates all domain users.                                       |
| `queryuser <RID>`         | Provides information about a specific user.                        |

# SMBMap
```shell-session
smbmap -H 10.129.14.128
```
we can use smbmap to see the list of permissions for each shared folder
use `-r sharename` to browse directories
`--download "sharename\filename"`
`--upload filepath-in-current-host "sharename:filename"`

checking access to share
```shell-session
smbmap -u forend -p Klmcargo2 -d INLANEFREIGHT.LOCAL -H 172.16.5.5
```
recursively list all directories 
```
smbmap -u forend -p Klmcargo2 -d INLANEFREIGHT.LOCAL -H 172.16.5.5 -R 'Department Shares' --dir-only
```

# CrackMapExec
```shell-session
crackmapexec smb 10.129.14.128 --shares -u '' -p ''
```

# Enum4Linux
```shell-session
./enum4linux-ng.py 10.129.14.128 -A -C 
```