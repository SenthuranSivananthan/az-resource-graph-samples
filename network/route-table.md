## Subnets without User Defined Route Table

Requirements: [PowerShell](https://docs.microsoft.com/en-us/azure/governance/resource-graph/first-query-powershell)

```powershell
$rgQuery = "where type == 'microsoft.network/virtualnetworks' | summarize subnets = make_list(properties.subnets)"
$results = Search-AzGraph -Query $rgQuery

$SubnetsWithoutUDR = [System.Collections.ArrayList]@()

foreach ($subnet in $results.subnets)
{
    if ($subnet.properties.routeTable -eq $null)
    {
        $captures = [regex]::Match($subnet.id, '/subscriptions/(.*)/resourceGroups/(.*)/providers/.*/virtualNetworks/(.*)/subnets/(.*)').Captures
   
        $item = New-Object PSObject
        $item | Add-Member NoteProperty SubscriptionId ($captures.Groups[1].value)
        $item | Add-Member NoteProperty ResourceGroupName ($captures.Groups[2].value)
        $item | Add-Member NoteProperty VNetName ($captures.Groups[3].value)
        $item | Add-Member NoteProperty SubnetName ($captures.Groups[4].value)

        $SubnetsWithoutUDR.Add($item)
    }
}

$SubnetsWithoutUDR | Format-Table
```
