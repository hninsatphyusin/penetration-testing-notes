when we are limited to a windows network and may not be able to use SSH for pivoting 

uses dynamic virtual channel from remote desktop service feature of windows

Binaries we need (downloaded into desktop alr): 
1. SocksOverRDP x64 Binaries - SocksOverRDPx64.zip
2. Proxifier Portable Binary - ProxifierPE.zip

Steps 
Pivot Machine
u might have to disable virus and threat protection settings and then run powershell as administrator
```cmd-session
Desktop\SocksOverRDP-x64> regsvr32.exe SocksOverRDP-Plugin.dll
```

then we can use `mstsc.exe` to rdp over new victim host and then transfer the socksoverrdp.zip again over to the new victim host.

start the socksoverrdp server with admin privileges 

confirm that the socs listern has start in the pivot machine
```cmd-session
netstat -antb | findstr 1080
```

Configure Proxifier
We open Proxifer -> Profile -> Proxy Servers -> Add -> Adddres 127.0.0.1. Socks Version 5 

For better rdp experience 
access the `Experience` tab in mstsc.exe and set `Performance` to `Modem`.