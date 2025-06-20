
# Subdomain Brute Forcing 
When you can't zone transfer, you have no choice but to brute force the subdomains 
```shell-session
for sub in $(cat /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.ns1.inlanefreight.htb @134.209.24.248 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done
```
## Alternate tools: DNSenum (https://github.com/fwaeytens/dnsenum)
```shell-session
dnsenum --dnsserver 10.129.224.217 --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/fierce-hostlist.txt app.inlanefreight.htb
```

