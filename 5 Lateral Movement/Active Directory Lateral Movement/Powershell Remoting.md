Bloodhound
go bloodhound if we gained control over a user through an attack such LLMNR/NBT-NS REsponse Spoofing or Kerberoasting. (Execution Rights on the Node Info tab) Or use pre-built queries `Find Workstations where Domain Users can RDP` or `Find Servers where Domain Users can RDP`.

can also check for winRM access 
```powershell-session
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Management Users"
```
ca01
db01
FILE
ctx1
ws01



bloodhound cypher query for winRM access
```cypher
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:CanPSRemote*1..]->(c:Computer) RETURN p2
```
then we can try to get into the [[winrm]] session