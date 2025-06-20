
## Dangerous Settings
| **Setting**               | **Description**                                                                          |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| `auth_debug`              | Enables all authentication debug logging.                                                |
| `auth_debug_passwords`    | This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged. |
| `auth_verbose`            | Logs unsuccessful authentication attempts and their reasons.                             |
| `auth_verbose_passwords`  | Passwords used for authentication are logged and can also be truncated.                  |
| `auth_anonymous_username` | This specifies the username to be used when logging in with the ANONYMOUS SSL mechanism. |
### nmap 
```shell-session
sudo nmap 10.129.240.87 -sV -p110,143,993,995 -sC
```

## cURL password enumeration? 
```shell-session
curl -k 'pop3s://10.129.240.87' --user robin:robin -v
```

Servers encrypted with SSL 
```shell-session
openssl s_client -connect 10.129.108.117:pop3s
```

10.129.108.117

can login with telnet also
```
telnet ip.addr port
```