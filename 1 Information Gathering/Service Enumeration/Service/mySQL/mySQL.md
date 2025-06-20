Usually runs TCP port 3306

`MySQL` default system schemas/databases:

- `mysql` - is the system database that contains tables that store information required by the MySQL server
- `information_schema` - provides access to database metadata
- `performance_schema` - is a feature for monitoring MySQL Server execution at a low level
- `sys` - a set of objects that helps DBAs and developers interpret data collected by the Performance Schema


## Enumeration 

```shell-session
sudo nmap 10.129.144.5 -sV -sC -p3306 --script mysql*
```
