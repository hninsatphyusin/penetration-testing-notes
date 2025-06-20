# Configuration 
Files: 
1. Local DNS configuration files
2. Zone Files 
3. Reverse name resolution files

## Dangerous Settings 
|**Option**|**Description**|
|---|---|
|`allow-query`|Defines which hosts are allowed to send requests to the DNS server.|
|`allow-recursion`|Defines which hosts are allowed to send recursive requests to the DNS server.|
|`allow-transfer`|Defines which hosts are allowed to receive zone transfers from the DNS server.|
|`zone-statistics`|Collects statistical data of zones.|
zone-transfer refers to the transfer of zones to another server in DNS, which generally happens over TCP port 53
