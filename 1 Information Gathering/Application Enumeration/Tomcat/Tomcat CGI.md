## identification
It has to have Apache Tomcat Running 
1. default directory for CGI scripts is `/cgi`

```shell-session
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.129.204.227:8080/cgi/FUZZ.cmd
```

```shell-session
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.129.204.227:8080/cgi/FUZZ.bat
```

