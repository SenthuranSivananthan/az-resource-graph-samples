## Virtual Machines with IP Forwarding enabled on the network interfaces

Azure Reference: [Enable or disable IP forwarding](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface#enable-or-disable-ip-forwarding)

IP forwarding enables the virtual machine a network interface is attached to:

* Receive network traffic not destined for one of the IP addresses assigned to any of the IP configurations assigned to the network interface.
* Send network traffic with a different source IP address than the one assigned to one of a network interface's IP configurations.

```sql
where type == "microsoft.network/networkinterfaces" and properties.enableIPForwarding == false
| extend vmResourceGroup = extract("/subscriptions/.*/resourceGroups/(.*)/providers/.*", 1, tostring(properties.virtualMachine.id))
| extend vmName = extract("/subscriptions/.*/virtualMachines/(.*)", 1, tostring(properties.virtualMachine.id))
| project subscriptionId, name, vmResourceGroup, vmName, location
```
