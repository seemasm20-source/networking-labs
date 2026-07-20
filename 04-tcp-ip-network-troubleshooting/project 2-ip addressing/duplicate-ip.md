
## 🔴 IP Issue 5 - Duplicate IP Address





## 📋 Problem Summary

Two devices on the same network share the same IP address. Both experience intermittent connectivity

drops, random failures and unreliable pings. The network cannot determine which device to send replies to.





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

### Step 1: Check the IP Configuration

Open the Command Prompt on each PC and run:

`ipconfig /all`

Check the IPv4 address, subnet mask, default gateway, and DHCP status to identify whether the devices are using the same IP address.

### Step 2: Check the ARP Table

Run:

`arp -a`

This command displays the IP-to-MAC address mappings stored in the ARP cache. If a suspected IP address is associated with 

different MAC addresses at different times,it may indicate a duplicate IP address conflict.



## 🔧 Quick Fix


Change one device to a unique IP:

→ Set to DHCP to receive unique IP automatically

→ OR assign different static IP not in use





## 🔗 Full Lab Documentation

This scenario was fully documented in the DHCP Configuration Portfolio including:

✅ Complete Packet Tracer lab setup

✅ How to create the duplicate IP conflict

✅ Step-by-step fix with CLI commands

✅ Verification screenshots

✅ Real-world help desk ticket
              
→ View full lab here:


[IP Address Conflict (Static vs DHCP) Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/ip-conflict.md)
