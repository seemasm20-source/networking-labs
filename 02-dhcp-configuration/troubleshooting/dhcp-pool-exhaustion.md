
Troubleshooting Issue- 2 



📋 Problem Summary

A new PC connects to the network but cannot receive an IP address. The DHCP pool has run out of available addresses all IPs are already assigned to existing devices. The new PC 

shows 0.0.0.0 or self-assigns a 169.254.x.x APIPA address.





## What is DHCP Pool Exhaustion?

DHCP Pool Exhaustion occurs when all available IP addresses in a DHCP pool have been assigned to devices, leaving no free addresses for new clients.

As a result, new devices cannot obtain an IP address from the DHCP server and may experience network connectivity issues.

### Example

DHCP Pool Range:

```text
192.168.10.10 - 192.168.10.15
```

Assigned Addresses:

```text
PC1 → 192.168.10.10
PC2 → 192.168.10.11
PC3 → 192.168.10.12
PC4 → 192.168.10.13
PC5 → 192.168.10.14
PC6 → 192.168.10.15
```

All available addresses have been leased.

When a new device (PC7) requests an IP address, the DHCP server cannot provide one because the pool has no remaining addresses.


















🔧 How to Create the Problem in Packet Tracer:


