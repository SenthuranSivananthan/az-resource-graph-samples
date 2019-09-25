## Query OS Name

```sql
where type == "microsoft.compute/virtualmachines"
| summarize count() by tostring(properties.storageProfile.imageReference.offer), tostring(properties.storageProfile.imageReference.sku)
| order by count_ desc
```
