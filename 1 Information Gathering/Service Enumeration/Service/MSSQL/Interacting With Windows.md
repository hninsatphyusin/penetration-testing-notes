## sqlcmd
```cmd-session
sqlcmd -S 10.129.20.13 -U username -P Password123
```
need to execute `G0` after every query to execute SQL syntax 

if we don't specify domain/hostname of target machine -> assume SQL Authentication and authenticate against users created in the SQL Server

Define domain/hostname -> Windows Authenticaiton

## sqsh
```
sqsh -S 10.129.203.7 -U .\\julio -P 'MyPassword!' -h
```
`.\\acountname` -> localhost 
`SERVERNAME\\accountname`

## powershell 
```powershell-session
Get-SQLQuery -Verbose -Instance "172.16.5.150,1433" -username "inlanefreight\damundsen" -password "SQL1234!" -query 'Select @@version'
```