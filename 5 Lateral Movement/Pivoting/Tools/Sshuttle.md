only works for pivoting over SSH and does not provide other options for pivoting over TOR or HTTPS proxy servers
```shell-session
sudo sshuttle -r ubuntu@10.129.202.64 172.16.5.0/23 -v 
```
with this command, sshuttle creates an entry in our ip tables to redirect all traffic to the 172.16.5.0/23 network through the pivot host

can do nmap normally now
