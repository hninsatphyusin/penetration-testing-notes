fast scanning 
```
sudo nmap $IP -p- -vv -n -Pn -T4
```
This searches all ports, with a verbose output, no DNS resolution, and no ping. After this one outputs the ports, follow up with:

```
nmap $IP -pall,the,ports -vv -n -Pn -sC -sV 
```
