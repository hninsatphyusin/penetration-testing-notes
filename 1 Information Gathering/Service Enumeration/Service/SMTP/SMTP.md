Protocol for sending emails in an IP network 
Often Combined with [[IMAP]] or [[POP3]] to fetch/send emails 

Ports:25, 587, 465(for encryption)

Agents Within a SMTP client
Mail User Agent (MUA): convert mail into a header and body and uploads both to the SMTP server 
Mail Transfer Agent (MTA): checks size, spam and stores the mail 
Mail Submission Agent (MSA): checks the validity, origin of the mail 
Mail Delivery Agent (MDA): transfers email to the recipient's mailbox
  

|Client (`MUA`)|`➞`|Submission Agent (`MSA`)|`➞`|Open Relay (`MTA`)|`➞`|Mail Delivery Agent (`MDA`)|`➞`|Mailbox (`POP3`/`IMAP`)|
|---|---|---|---|---|---|---|---|---|

# Configuration 
file 
```shell-session
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"
```


# Footprinting 
```shell-session
sudo nmap 10.129.14.128 -sC -sV -p25
```

To check for open relay 
```shell-session
sudo nmap 10.129.29.248 -p25 --script smtp-open-relay -v
```
