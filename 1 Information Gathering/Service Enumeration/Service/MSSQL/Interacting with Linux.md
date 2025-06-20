## mssqlclient.py
```shell-session
impacket-mssqlclient username@10.129.162.213 -windows-auth
```

```shell-session
select name from sys.databases
```

```
USE databasename;
SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE = 'BASE TABLE';
SELECT * FROM employee_information;
```

## mssqlclient.py
```
mssqlclient.py -p 1433 julio@10.129.203.7 
```

```shell-session
mssqlclient.py INLANEFREIGHT/DAMUNDSEN@172.16.5.150 -windows-auth
```

## sqsh
```shell-session
sqsh -S 10.129.20.13 -U username -P Password123
```

