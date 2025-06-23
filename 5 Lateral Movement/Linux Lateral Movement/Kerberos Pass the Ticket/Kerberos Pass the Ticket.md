
stored in `/tmp` directory 
in environment variable `KRB5CCNAME`
keytab files also contain pairs of kerberos principals and encrypted keys (derived from kerberos password) -- which can be used to authenticate to various remote systems using Kerberos without entering a password

## How to identify if a Linux Machine is in a domain
```
realm list
ps -ef | grep -i "winbind\|sssd"
```


