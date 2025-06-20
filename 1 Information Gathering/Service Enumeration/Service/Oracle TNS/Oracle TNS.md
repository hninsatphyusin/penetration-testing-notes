Oracle Transparent Network Substrate
Communication protocol that faciliates communication between Oracle databases and applications over networks. 

Preferred solution for managing large, complex databases in healthcare, finance and retail industries. 

Default port: TCP/1521 

Default password: dbsnmp 

finger service with oracle -> risky 

Footprinting 
```
./odat.py -h 
```


```shell-session
sudo nmap -p1521 -sV 10.129.204.235 --open
```