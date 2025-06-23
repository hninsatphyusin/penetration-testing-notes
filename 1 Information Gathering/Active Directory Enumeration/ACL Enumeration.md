# PowerView 
```
Find-InterestingDomainAcl
```
might take a while to read all of those, not good in a time-boxed assessment 

ACL Enumeration by user
```
Import-Module .\PowerView.ps1

$sid = Convert-NameToSid username

Get-DomainObjectACL -Identity * | ? {$_.SecurityIdentifier -eq $sid}

Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $sid} 
```
now we see the ObjectAceType and then Google it to see what abilities it has
(we might have to open a new powershell session whenever there is an error)

reverse search objectacetype guid 
```
$guid= "00299570-246d-11d0-a768-00aa006e0529"

Get-ADObject -SearchBase "CN=Extended-Rights,$((Get-ADRootDSE).ConfigurationNamingContext)" -Filter {ObjectClass -like 'ControlAccessRight'} -Properties * |Select Name,DisplayName,DistinguishedName,rightsGuid| ?{$_.rightsGuid -eq $guid} | fl
```
but this is not very efficient either (just use the second get-domainobjectacl command)

How to see what other accounts the ACE can control from our acc


Getting a list of domain users
```powershell-session
Get-ADUser -Filter * | Select-Object -ExpandProperty SamAccountName > ad_users.txt
```

```
foreach($line in [System.IO.File]::ReadLines("C:\tools\ad_users.txt")) {get-acl  "AD:\$(Get-ADUser $line)" | Select-Object Path -ExpandProperty Access | Where-Object {$_.IdentityReference -match 'INLANEFREIGHT\\forend'}}
```
then we do this whole enumeration using the new account that we have gotten 

checking a single account
```
Get-ACL "AD:\$(Get-ADUser victim)" | 
    Select-Object -ExpandProperty Access | 
    Where-Object { $_.IdentityReference -match 'INLANEFREIGHT\\bully' }
```

checking a group 
```
$dn = (Get-ADGroup "GPO Management").DistinguishedName
Get-ACL "AD:$dn" | 
    Select-Object -ExpandProperty Access | 
    Where-Object { $_.IdentityReference -match 'INLANEFREIGHT\\forend' }

```



If the user is in a group, see what the group can do -> seee if its is a nested group and then try to find the parent group

```
Get-DomainGroup -Identity "Help Desk Level 1" | select memberof

$itgroupsid = Convert-NameToSid "Information Technology"

Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $itgroupsid} -Verbose
```


# Bloodhound 
use sharphound to get all the data first 
```
.\SharpHound.exe -c All --zipfilename ILFREIGHT
```

starting bloodhound
neo4j user->neo4j pass->BloodHound
bloodhound: admin, password -> saved on firefox

open bloodhound by typing bloodhound into the 
the bloodhound version and the sharphound version must match, i have the most recent one installed in desktop


##  Method 1
1. Set first user as our starting node -> go to Node Info tab and scroll down to Outbound Control Rights
2. click 1 next to First Degree Object Control -> we can see what ACE and what user this current user has control over

How to know how to abuse this ACE: 
right click on the line between two objects -> select HELP 

Then we can click on 16 next to Transitive Object Control to see the potential attack path 

## METHOD 2
go to cypher, click on shortest path to domain admins