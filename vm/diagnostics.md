## Identify unique storage accounts used for boot diagnostics

```sql
where type == "microsoft.compute/virtualmachines"
| where notnull(properties.diagnosticsProfile.bootDiagnostics.storageUri)
| distinct tostring(properties.diagnosticsProfile.bootDiagnostics.storageUri)
```
## Identify number of virtual machines by storage account

```sql
where type == "microsoft.compute/virtualmachines"
| where notnull(properties.diagnosticsProfile.bootDiagnostics.storageUri)
| project name, bootDiagStorageAccount=properties.diagnosticsProfile.bootDiagnostics.storageUri
| summarize count() by tostring(bootDiagStorageAccount)
```
## List all VMs used by each storage account

```sql
where type == "microsoft.compute/virtualmachines"
| where notnull(properties.diagnosticsProfile.bootDiagnostics.storageUri)
| project name, subscriptionId, bootDiagStorageAccount=properties.diagnosticsProfile.bootDiagnostics.storageUri
| summarize vmList=make_set(name) by subscriptionId, tostring(bootDiagStorageAccount)
| project subscriptionId, tostring(bootDiagStorageAccount), vmCount=array_length(vmList), vmList
| order by vmCount asc
```
