# Windows Defender 
will block tools such as PowerView 

use powershell to get current defender status
```
Get-MpComputerStatus
```
if `RealTimeProtectionEnabled` is `True` that means Defender is enabled on the system


# AppLocker
application whitelisting 
organisation often block cmd.exe and powershell.exe and write access to certain directories 

However they often forget about other powershell executable locations
```
%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
```

```
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

# Powershell Constrained Language Mode
locks down many features needed to use powershell effectively such as blocking COM objects, only allowing approved .NET types, XAML-based workflows, Powershell classes, and more. 
execute in powershell:
```
$ExecutionContext.SessionState.LanguageMode
```

# LAPS
Local Administrator Password Solution 
randomise and rotate local administrator passwords on Windows hosts and prevent lateral movement 

in powershell
```
Find-LAOSDelegatedGroups
```
checking rights on each comouter and for any groups with access and users with All Extended Rights
```
Find-AdmPwdExtendedRights
```
search for computers that have LAPS enabled when passwords expire
```
Get-LAPSComputers
```

# Downgrading powershell
powershell 2.0 or older don't have event logging 
there may be multiple version of powershell on the computer
```
Get-host
powershell.exe -version 2
Get-host
get-module
```

# firewall check 
```powershell-session
PS: netsh advfirewall show allprofiles
cmd: sc query windefend
```

Check if there are ppl logged on on the computer also
```
qwinsta
```
