#file-system #nas #data

### WHEN MAKES SENSE

|Use case|Recommended|
|---|---|
|Single Pi sharing one drive|❌ Simpler to use NFS/Samba|
|Want redundancy between Pis|✅ Gluster replica volume|
|Want to expand storage later|✅ Gluster distributed volume|
|Temporary or removable drives|⚠️ Works, but rebalancing required|
|Mostly backups or large media|✅ Perfect fit|
|Random access workloads|❌ Use local SSD or NFS instead|


### PERFORMACE IMPACT

|Factor|Effect|Notes|
|---|---|---|
|**Idle**|Very low|Glusterd just idles, no polling load|
|**Network I/O**|Higher than NFS on single node|Because metadata and replication are coordinated|
|**Caching**|Very effective|Gluster clients cache reads and metadata|
|**Write speed (replica)**|Lower than NFS if replication enabled|Each write is duplicated|
|**Read speed (distributed)**|Good|Parallel reads scale well|

