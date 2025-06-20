windows version for web services management protocol 


used for remote management of windows systems 

POrts: TCP 5985 HTTP, 5986 HTTPS

can use Evil-WinRM to communicate with a WinRM Service

```
evil-winrm -i <target-IP> -u <username> -p <password>
```

from windows powershell
```powershell-session
$password = ConvertTo-SecureString "Klmcargo2" -AsPlainText -Force

$cred = new-object System.Management.Automation.PSCredential ("INLANEFREIGHT\forend", $password)

Enter-PSSession -ComputerName ACADEMY-EA-MS01 -Credential $cred
```