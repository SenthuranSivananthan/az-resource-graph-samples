## Public IP Addresses

```
where type == "microsoft.network/publicipaddresses"
| where notnull(properties.ipAddress)
| project subscriptionId, resourceGroup, name, location, properties.ipAddress
```
