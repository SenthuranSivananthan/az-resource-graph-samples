## Subnets without Network Security Groups

```powershell
$rgQuery = "where type == 'microsoft.network/virtualnetworks' | summarize subnets = make_list(properties.subnets)"
$results = Search-AzGraph -Query $rgQuery

$SubnetsWithoutNSGs = [System.Collections.ArrayList]@()

foreach ($subnet in $results.subnets)
{
    if ($subnet.properties.networkSecurityGroup -eq $null)
    {
        $captures = [regex]::Match($subnet.id, '/subscriptions/(.*)/resourceGroups/(.*)/providers/.*/virtualNetworks/(.*)/subnets/(.*)').Captures
   
        $item = New-Object PSObject
        $item | Add-Member NoteProperty SubscriptionId ($captures.Groups[1].value)
        $item | Add-Member NoteProperty ResourceGroupName ($captures.Groups[2].value)
        $item | Add-Member NoteProperty VNetName ($captures.Groups[3].value)
        $item | Add-Member NoteProperty SubnetName ($captures.Groups[4].value)

        $SubnetsWithoutNSGs.Add($item)
    }
}

$SubnetsWithoutNSGs | Format-Table
```
