PowerView 
Enumerating remote desktop users group
```
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"
```

Bloodhound
go bloodhound if we gained control over a user through an attack such LLMNR/NBT-NS REsponse Spoofing or Kerberoasting. (Execution Rights on the Node Info tab) Or use pre-built queries `Find Workstations where Domain Users can RDP` or `Find Servers where Domain Users can RDP`.
