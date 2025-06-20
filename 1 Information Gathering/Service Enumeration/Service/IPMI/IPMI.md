Intelligent Platform Management Interface (IPMI)

Set of standardised specifications for hardware-based host management systems used for system management and monitoring 

Ability to manage and monitor systems even if they are powered off or in an unresponsive state. 

Default Port: 623/UDP 

Use IPMI to get access to BMC (Baseboard Management Controllers) -> full access to the host motherboard, reboot, power off, or even reinstall OS

## Finding IPMI version
```shell-session
sudo nmap -sU --script ipmi-version -p 623 10.129.105.148
```
can use Metasploit too

Default Credentials 

|Product|Username|Password|
|---|---|---|
|Dell iDRAC|root|calvin|
|HP iLO|Administrator|randomized 8-character string consisting of numbers and uppercase letters|
|Supermicro IPMI|ADMIN|ADMIN|
For HP iLO:
```
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
```

Flaw in IPMI 2.0 
Uses RAKP protocol, server sends a salted SHA1 or MD5 hash of the user's password to the client before authentication takes place. 
Passowrd hashes can then be cracked offline using a dictionary attack using Hashcat mode 7300

## Getting IPMI hashes
search scanner 
Metasploit IPMI 2.0 RAKP Remote SHA1 Password Hash Retrieval 


```
hashcat \
  --backend-devices 1 \
  --attack-mode 0 \
  --workload-profile 3 \
  --optimized-kernel-enable \
  --hash-type 7300 \
  --username \
  --session ipmi \
  --outfile hashcat_cracked \
  ipmi.txt \
  /usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt
```