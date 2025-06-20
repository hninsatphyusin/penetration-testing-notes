# Enumerating SMTP users 
metasploit
set RHOSTS and wordlist
```
msfconsole 
search scanner smtp enum 
use 1 
exploit 
```

![[footprinting-wordlist 1.txt]]

# Evolution
GUI
Evolution -> can send and receive msgs (so both smtp and pop3 ig)

```shell-session
sudo apt-get install evolution
```

Note: If an error appears when starting evolution indicating "bwrap: Can't create file at ...", use this command to start evolution `export WEBKIT_FORCE_SANDBOX=0 && evolution`.

Settings u need to put: 
- Identity 
	- Name
	- Email
- REceiving email
	- server type (imap or pop)
	- server (and port)
	- username
	- encryption method (no encryption)
- Sending email
	- server (and port)
	- server requires authentication
	- no encryption
	- authenticate with username


# Mail Xchange records
```
host -t MX domain.name

dig mx domain.name | grep "MX" | grep -v ";"
```
from this result we can see what ail servers you used (i.e. google, microsoft, zoho etc)

A (address) records
```
host -t A mail1.inlanefreight.htb.
```
take note here this is a subdomain of the mail server
