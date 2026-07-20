
## 🔴 IP Issue 5 - Duplicate IP Address





## 📋 Problem Summary

Two devices on the same network share the same IP address. Both experience intermittent connectivity

drops, random failures and unreliable pings. The network cannot determine which device to send

replies to.





##  🔍 Quick Overview



Duplicate IP symptoms:

→ Random connectivity drops
→ Ping replies inconsistent
→ One or both devices affected
→ Issue clears temporarily then returns

Common causes:
→ Static IP assigned within DHCP pool range

→ One device manually given same static IP
→ DHCP excluded-address range too small





## 🔎 Quick Verify

Step :1 Go to each Pcs command prompt and give ipconfig/all and see the IP details.

Step:2 C:\> arp -a You can also check two different MACs for same IP address and by this you can confirm duplicate IP 


## 🔧 Quick Fix


Change one device to a unique IP:

→ Set to DHCP to receive unique IP automatically

→ OR assign different static IP not in use

Prevent recurrence:

→ Exclude static IPs from DHCP pool: Router(config)# ip dhcp excluded-address 192.168.10.10




## 🔗 Full Lab Documentation

This scenario was fully documented in the DHCP Configuration Portfolio including:

✅ Complete Packet Tracer lab setup

✅ How to create the duplicate IP conflict

✅ Step-by-step fix with CLI commands

✅ Verification screenshots

✅ Real-world help desk ticket
              
→ View full lab here:
