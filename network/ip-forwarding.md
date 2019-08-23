## Virtual Machines with IP Forwarding enabled on the network interfaces

```sql
where type == "microsoft.network/networkinterfaces" and properties.enableIPForwarding == false
| extend vmResourceGroup = extract("/subscriptions/.*/resourceGroups/(.*)/providers/.*", 1, tostring(properties.virtualMachine.id))
| extend vmName = extract("/subscriptions/.*/virtualMachines/(.*)", 1, tostring(properties.virtualMachine.id))
| project subscriptionId, name, vmResourceGroup, vmName, location
```
