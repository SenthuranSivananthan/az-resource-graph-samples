## Virtual networks without DDOS Standard

```sql
where type == "microsoft.network/virtualnetworks" and properties.enableDdosProtection == false
 | project subscriptionId, resourceGroup, name, location
```
