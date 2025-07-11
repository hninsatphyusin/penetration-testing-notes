Logging in 
```shell-session
mysql -u root -pP4SSw0rd -h 10.129.14.128 -P PORT
```
might have to use --ssl-verify-server-cert=FALSE, if there is an error about ssl certifcates. 

Show tables, information and metadata
```
mysql> use sys;
mysql> show tables;  
mysql> select host, unique_users from host_summary;
```

General Commands

| **Command**                                          | **Description**                                                                                       |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `mysql -u <user> -p<password> -h <IP address>`       | Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password. |
| `show databases;`                                    | Show all databases.                                                                                   |
| `use <database>;`                                    | Select one of the existing databases.                                                                 |
| `show tables;`                                       | Show all available tables in the selected database.                                                   |
| `show columns from <table>;`                         | Show all columns in the selected database.                                                            |
| `select * from <table>;`                             | Show everything in the desired table.                                                                 |
| `select * from <table> where <column> = "<string>";` | Search for needed `string` in the desired table.                                                      |
