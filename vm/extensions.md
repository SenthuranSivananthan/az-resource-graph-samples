## Find extensions installed on Virtual Machines

```sql
where type == "microsoft.compute/virtualmachines/extensions"
| parse id with * "/providers/Microsoft.Compute/virtualMachines/" vmName "/extensions/" *
| project subscriptionId, resourceGroup, location, vmName, name
| summarize vmExtensions=make_set(name) by subscriptionId, resourceGroup, location, vmName
```

## Find VMs without a specific extension

```sql
where type == "microsoft.compute/virtualmachines/extensions"
| parse id with * "/providers/Microsoft.Compute/virtualMachines/" vmName "/extensions/" *
| project subscriptionId, resourceGroup, location, vmName, name
| summarize vmExtensions=make_set(name) by subscriptionId, resourceGroup, location, vmName
| where vmExtensions !contains_cs "MicrosoftMonitoringAgent"
```

## Find VMs with a specific extension

```sql
where type == "microsoft.compute/virtualmachines/extensions"
| parse id with * "/providers/Microsoft.Compute/virtualMachines/" vmName "/extensions/" *
| project subscriptionId, resourceGroup, location, vmName, name
| summarize vmExtensions=make_set(name) by subscriptionId, resourceGroup, location, vmName
| where vmExtensions contains_cs "MicrosoftMonitoringAgent"
```
