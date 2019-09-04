## Key Vaults without soft delete

```sql
where type =~ "microsoft.keyvault/vaults" and (isnull(properties.enableSoftDelete) or properties.enableSoftDelete == false)
```
