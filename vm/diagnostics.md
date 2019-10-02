## Identify unique storage accounts used for boot diagnostics

```sql
where type == "microsoft.compute/virtualmachines"
| where notnull(properties.diagnosticsProfile.bootDiagnostics.storageUri)
| distinct tostring(properties.diagnosticsProfile.bootDiagnostics.storageUri)
```
