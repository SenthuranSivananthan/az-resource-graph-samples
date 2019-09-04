## Key Vaults without soft delete

Azure Reference: [Azure Key Vault soft-delete overview](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-soft-delete)

Key Vault's soft delete feature allows recovery of the deleted vaults and vault objects, known as soft-delete. Specifically, we address the following scenarios:

* Support for recoverable deletion of a key vault
* Support for recoverable deletion of key vault objects (ex. keys, secrets, certificates)

```sql
where type =~ "microsoft.keyvault/vaults" and (isnull(properties.enableSoftDelete) or properties.enableSoftDelete == false)
```
