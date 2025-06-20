
Starting the telnet session 
```shell-session
telnet 10.129.14.128 25
```

  After which can use the commands followed by the email adddress

|**Command**|**Description**|
|---|---|
|`AUTH PLAIN`|AUTH is a service extension used to authenticate the client.|
|`HELO`|The client logs in with its computer name and thus starts the session.|
|`MAIL FROM`|The client names the email sender.|
|`RCPT TO`|The client names the email recipient.|
|`DATA`|The client initiates the transmission of the email.|
|`RSET`|The client aborts the initiated transmission but keeps the connection between client and server.|
|`VRFY`|The client checks if a mailbox is available for message transfer.|
|`EXPN`|The client also checks if a mailbox is available for messaging with this command.|
|`NOOP`|The client requests a response from the server to prevent disconnection due to time-out.|
|`QUIT`|The client terminates the session.|

```
HELO mail1.inlanefreight.htb 
EHLO mail1.inalnefreight.htb
```

Verify the users that exists 
May or may not work 
```
VRFY root
VRFY cryp0l1t3
VRFY testuser

EXPN john 
EXPN support-team
EXPN all
```

Can send email by specifying MAIL FROM, RCPT TO< DATA etc 
