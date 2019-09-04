## List of AKS clusters

```sql
where type == "microsoft.containerservice/managedclusters"
| project
	subscriptionId,
	resourceGroup,
	name,
	location,
	networkPolicy = properties.networkProfile.networkPolicy,
	k8sversion = properties.kubernetesVersion,
	fqdn=properties.fqdn,
	dnsPrefix = properties.dnsPrefix,
	spnClientId = properties.servicePrincipalProfile.clientId,
	rbac = properties.enableRBAC,
	aadServerAppId = properties.aadProfile.serverAppID,
	aadClientAppId = properties.aadProfile.clientAppID,
	aadTenantId = properties.aadProfile.tenantID
```
