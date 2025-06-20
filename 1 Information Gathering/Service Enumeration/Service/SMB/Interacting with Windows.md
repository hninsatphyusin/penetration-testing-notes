# run.exe
```
\\ip.address\sharename
```

# cmd
connecting to smb
```
dir \\ip.address\sharename
```

mounting on N without credentials
```
net use n: \\ip.address\sharename
```

mounting on N with credentials
```
net use n: \\192.168.220.129\Finance /user:user Password123
//them u have to go the n: its mounting the smb on n:
```

# powershell
connecting to smb 
```
Get-ChildItem \\192.168.220.129\Finance\
```

mount on N without credentials
```
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem"
```

mount on N with credentials
```
$username = 'plaintext'
$password = 'Password123'
$secpassword = ConvertTo-SecureString $password -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential $username, $secpassword
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred
```