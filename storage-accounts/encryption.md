## Storage accounts with unencrypted traffic 

```sql
where type == "microsoft.storage/storageaccounts" and properties.supportsHttpsTrafficOnly == false
| project subscriptionId, location, resourceGroup, name, kind
```

## Storage accounts with unencrypted data at rest - blobs

```sql
where type == "microsoft.storage/storageaccounts" and properties.encryption.services.blob.enabled == false
| project subscriptionId, location, resourceGroup, name, kind
```

## Storage accounts with unencrypted data at rest - files

```sql
where type == "microsoft.storage/storageaccounts" and properties.encryption.services.file.enabled == false
| project subscriptionId, location, resourceGroup, name, kind
```
