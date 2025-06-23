
# Windows 
CMD
```
systeminfo | findstr /B "Domain"
```
POWERSHELL 
```
(Get-WmiObject Win32_ComputerSystem).PartOfDomain

(Get-WmiObject Win32_ComputerSystem).Domain
```

# Linux
```
realm list
```

```
kinit -k host/$(hostname -f)
```