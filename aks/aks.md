## List of AKS clusters

```sql
where type == "microsoft.containerservice/managedclusters"
| project subscriptionId, resourceGroup, name, properties.kubernetesVersion, properties.fqdn, properties.dnsPrefix, properties.servicePrincipalProfile.clientId, properties.enableRBAC
```