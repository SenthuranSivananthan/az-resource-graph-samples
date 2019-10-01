## List extensions installed on Virtual Machines

```sql
where type == "microsoft.compute/virtualmachines/extensions"
| parse id with * "/providers/Microsoft.Compute/virtualMachines/" vmName "/extensions/" *
| project subscriptionId, resourceGroup, location, vmName, name
| summarize vmExtensions=make_set(name) by subscriptionId, resourceGroup, location, vmName
```
