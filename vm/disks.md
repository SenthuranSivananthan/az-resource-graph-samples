## Query Disks

```sql
resources
| where type == "microsoft.compute/disks"
| project subscriptionId, resourceGroup, name, Tier=sku.name, SizeInGB=properties.diskSizeGB, SizeTier=properties.tier, zones, VM=managedBy
| order by subscriptionId, resourceGroup, VM
```
