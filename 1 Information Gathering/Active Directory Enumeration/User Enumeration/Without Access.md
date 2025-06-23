## Enumerating Users with Kerbrute 
uses Kerberos Pre-Authentication, which is much faster and potentially stealthier way to perform password spraying. Does not generate Windows event ID 4625: An account failed to log on, or a logon failure which is often monitored for when enumerating users. But when using that users list to do password spraying, a failed attempt will generate the logon failure windows event.

```shell-session
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt 
```
we might get a hash, that means that is vulnerable to [[ASREPRoasting](3%20Exploitation/Active%20Directory%20Attacks/ASREPRoasting.md)]
if the hash is not crackable by 18200 hashcat, generate the hash again by using kerbrute or another tool ike `impacket-GetNPUsers` 

file saving
```
kerbrute userenum -d htb.local --dc 10.10.10.161 /opt/jsmith.txt > results.txt
```

```
grep 'VALID USERNAME:' kerbrute_results.txt | awk '{print $4}' > usernames.txt
```

then we can do some password spraying with crackmapexec on smb 

### go google dorking to get pdf files from the website 

## LDAP Enumeration
```
nmap -p 389 --script ldap-search --script-args 'ldap.username="cn=ldaptest,cn=users,dc=cqure,dc=net",ldap.password=ldaptest,ldap.qfilter=users,ldap.attrib=sAMAccountName' 10.10.10.161
```

To list accounts, groups and computers from LDAP Server
```
enum4linux <IP_ADDRESS> | egrep "Account|Domain|Lockout|group"
```

### LDAPSearch
```
ldapsearch -x -H ldap://10.10.10.161 -D '' -w '' -b "DC=htb,DC=local"
```
- `-b "DC=<SUBDOMAIN>,DC=<TLD>"`: Sets the search base (e.g., DC=example,DC=com).
