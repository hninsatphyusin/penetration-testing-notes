```shell-session
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.135.203 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```
Python script for this: https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py