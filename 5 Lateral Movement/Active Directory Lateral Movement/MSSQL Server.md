# Bloodhound
cypher search to find users with SQL Admin Rights
```
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:SQLAdmin*1..]->(c:Computer) RETURN p2
```
using PowerUpSQL to enumerate MSSQL Instances 
```
Import-Module .\PowerUpSQL.ps1
Get-SQLInstanceDomain
```
then enumeration through [[MSSQL]] then try to attack the MSSQL service like [[SQL DBs]]
