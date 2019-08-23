## Virtual networks without DDOS Standard

```
where type == "microsoft.network/virtualnetworks"
 | where properties.enableDdosProtection == false
 | project subscriptionId, resourceGroup, name, location
```
