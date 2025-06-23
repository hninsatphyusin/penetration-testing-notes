# Workaround 1 PSCredential Object
We can also connect to the remote host via host A and set up a PSCredential object to pass our credentials again

```
$SecPassword = ConvertTo-SecureString 's3rvice' -AsPlainText -Force

$Cred = New-Object System.Management.Automation.PSCredential('HTB\svc-alfresco', $SecPassword)
```
then how we can use powerview to enum the domain 
make sure we use the -credential $Cred at all times
```
get-domainuser -spn -credential $Cred | select samaccountname
```

# Workaround #2: Register PSSession Configuration

```powershell-session
Register-PSSessionConfiguration -Name withCred -RunAsCredential HTB\svc-alfresco


Restart-Service WinRM

Enter-PSSession -ComputerName Foest -Credential HTB\svc-alfresco -ConfigurationName withCred
```
once u restart the winRM it will kick us out so we just need to rejoin the correct one with the configuration name

then we can run the commands normally
# Problem
using winrm/powershell to authenticate two different accounts in lateral movement


crux of the issue is that when using WinRM to authenticate over two or more connections, the user's password is never cached as part of their login


![[Screenshot 2025-06-18 at 11.37.40 PM.png]]
When we connect to `DEV01` using a tool such as `evil-winrm`, we connect with network authentication, so our credentials are not stored in memory and, therefore, will not be present on the system to authenticate to other resources on behalf of our user. 

When we load a tool such as `PowerView` and attempt to query Active Directory, Kerberos has no way of telling the DC that our user can access resources in the domain. This happens because the user's Kerberos TGT (Ticket Granting Ticket) ticket is not sent to the remote session; therefore, the user has no way to prove their identity, and commands will no longer be run in this user's context. In other words, when authenticating to the target host, the user's ticket-granting service (TGS) ticket is sent to the remote service, which allows command execution, but the user's TGT ticket is not sent. When the user attempts to access subsequent resources in the domain, their TGT will not be present in the request, so the remote service will have no way to prove that the authentication attempt is valid, and we will be denied access to the remote service.

