## All Public IP Addresses

```sql
where type == "microsoft.network/publicipaddresses" and notnull(properties.ipAddress)
| project subscriptionId, resourceGroup, name, location, properties.ipAddress
```
## Public IP Addresses attached to Virtual Machines

Requirements: [PowerShell](https://docs.microsoft.com/en-us/azure/governance/resource-graph/first-query-powershell)

```powershell
$rgQuery = "where type == 'microsoft.network/networkinterfaces' and properties.virtualMachine.id != ''"
$results = Search-AzGraph -Query $rgQuery

$VMsWithPublicIPs = [System.Collections.ArrayList]@()

foreach ($networkInterface in $results)
{
    foreach ($ipConfiguration in $networkInterface.properties.ipConfigurations)
    {
        if ($ipConfiguration.properties.publicIPAddress -ne $null)
        {
            $captures = [regex]::Match($networkInterface.properties.virtualMachine.id, '/subscriptions/(.*)/resourceGroups/(.*)/providers/Microsoft.Compute/virtualMachines/(.*)').Captures
   
            $item = New-Object PSObject
            $item | Add-Member NoteProperty SubscriptionId ($captures.Groups[1].value)
            $item | Add-Member NoteProperty ResourceGroupName ($captures.Groups[2].value)
            $item | Add-Member NoteProperty VMName ($captures.Groups[3].value)

            $VMsWithPublicIPs.Add($item)
        }
    }
}

$VMsWithPublicIPs | Format-Table
```
