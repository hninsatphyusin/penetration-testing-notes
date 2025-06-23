# Background
Many large organizations will acquire new companies over time and bring them into the fold. One way this is done for ease of use is to establish a trust relationship with the new domain. In doing so, you can avoid migrating all the established objects, making integration much quicker.

# Enumerating Trust Relationships 
```powershell-session
Import-Module activedirectory


Get-ADTrust -Filter *
```
active directory is preinstalled module

Check existsing trusts (import powerview)
```
Get-DomainTrust 


Get-DomainTrustMapping
```

Checking Users in child domain using get-domainuser
```
Get-DomainUser -Domain LOGISTICS.INLANEFREIGHT.LOCAL | select SamAccountName
```

alternative
```
netdom query /domain:inlanefreight.local trust

netdom query /domain:inlanefreight.local dc

netdom query /domain:inlanefreight.local workstation
```

can also use bloodhound to visualise these trust relationships using Map Domain Trusts pre-built query. 

