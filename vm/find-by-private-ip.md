## Find virtual machines by private ip

```sql
where type == "microsoft.network/networkinterfaces"
| summarize IPs = make_list(properties.ipConfigurations) by tostring(properties.virtualMachine.id)
| where IPs contains "10.10.10.10"
```
