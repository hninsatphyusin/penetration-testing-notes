custom wordlist generation
```shell-session
for i in $(seq 1 1000); do echo $i >> ids.txt; done
```

```shell-session
ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:5174/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```