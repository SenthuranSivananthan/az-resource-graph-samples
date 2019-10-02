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
