## Virtual networks without DDOS Standard

Azure Reference: [Azure DDoS Protection Standard overview](https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview)

DDoS Protection Standard can mitigate the following types of attacks:

* Volumetric attacks: The attack's goal is to flood the network layer with a substantial amount of seemingly legitimate traffic. It includes UDP floods, amplification floods, and other spoofed-packet floods. DDoS Protection Standard mitigates these potential multi-gigabyte attacks by absorbing and scrubbing them, with Azure’s global network scale, automatically.

* Protocol attacks: These attacks render a target inaccessible, by exploiting a weakness in the layer 3 and layer 4 protocol stack. It includes, SYN flood attacks, reflection attacks, and other protocol attacks. DDoS Protection Standard mitigates these attacks, differentiating between malicious and legitimate traffic, by interacting with the client, and blocking malicious traffic.

* Resource (application) layer attacks: These attacks target web application packets, to disrupt the transmission of data between hosts. The attacks include HTTP protocol violations, SQL injection, cross-site scripting, and other layer 7 attacks. Use the Azure Application Gateway web application firewall, with DDoS Protection Standard, to provide defense against these attacks. There are also third-party web application firewall offerings available in the Azure Marketplace.

```sql
where type == "microsoft.network/virtualnetworks" and properties.enableDdosProtection == false
 | project subscriptionId, resourceGroup, name, location
```
