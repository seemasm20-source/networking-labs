
## Troubleshooting Issue- 2 



## 📋 Problem Summary

A new PC connects to the network but cannot receive an IP address. The DHCP pool has run out of available addresses all IPs are already assigned to existing devices. 

The new PC shows 0.0.0.0 or self-assigns a 169.254.x.x APIPA address.





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


















## 🔧 How to Create the Problem in Packet Tracer:


 ## Step 1 :
 
Set up normal DHCP first




Router>enable

Router#configure terminal

Router(config)# interface GigabitEthernet0/1

Router(config-if)#ip address 192.168.20.1 255.255.255.0


Router(config-if)#no shutdown

Router(config-if)#exit

Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.9

Router(config)# ip dhcp excluded-address 192.168.20.13 192.168.20.254

Router(config)#ip dhcp pool LAN2_POOL

Router(dhcp-config)#network 192.168.20.0 255.255.255.0

Router(dhcp-config)#default-router 192.168.20.1

Router(dhcp-config)#dns-server 8.8.8.8










On each PC:

Desktop → IP Configuration → DHCP


PC4 gets 192.168.20.10 (screenshot attached)

PC5 gets 192.168.20.11

PC6 gets 192.168.20.12
























<img width="1920" height="1080" alt="Screenshot (335)" src="https://github.com/user-attachments/assets/c160fe96-2fb1-4483-ab4f-355fa396be7b" />






































## Step: 2

Shrink the pool to simulate exhaustion

Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.9

Router(config)# ip dhcp excluded-address 192.168.20.13 192.168.20.254

Router(config)# end

Router# write memory












<img width="1920" height="1080" alt="Screenshot (324)" src="https://github.com/user-attachments/assets/1641303d-236c-440f-a616-2387de27fb1d" />




























## Step 3:



Now add PC7 and set it to DHCP.

Since all available addresses are already leased, PC7 will not receive an IP address (or may eventually show an APIPA address 169.254.x.x).







| Device | IP Address    |
| ------ | ------------: |
| PC4    | 192.168.20.10 |
| PC5    | 192.168.20.11 |
| PC6    | 192.168.20.12 |
| PC7    | 169.254.x.x   |









## Step:4 



type show ip dhcp binding

This displays all IP addresses that the DHCP server has leased to clients.




| IP Address    | Client-ID/Hardware Address | Lease Expiration | Type      |
| ------------- | -------------------------- | ---------------- | --------- |
| 192.168.20.10 | 0090.0C57.2A40             | --               | Automatic |
| 192.168.20.11 | 00E0.F969.B81C             | --               | Automatic |
| 192.168.20.12 | 000D.BD58.3C5E             | --               | Automatic |


Note: This confirms that all available DHCP addresses are already leased.





















<img width="1920" height="1080" alt="Screenshot (325)" src="https://github.com/user-attachments/assets/8f7f8701-caa2-49da-aef6-af2e8977e780" />




























## Step:5 


Add new PC → PC7 in LAN B

Connect PC7 to Switch 2

Go to:

PC7 → Desktop → IP Configuration → DHCP

Expected Result

PC7 cannot obtain an IP address because the DHCP pool is exhausted. PC gets APIPA error
























<img width="1920" height="1080" alt="Screenshot (321)" src="https://github.com/user-attachments/assets/3db22e59-cf48-48e0-a832-5e68d6269271" />



















## Step:6 




## Fix the Problem

Increase the available range:

Router(config)# no ip dhcp excluded-address 192.168.20.13 192.168.20.254

Router(config)# ip dhcp excluded-address 192.168.20.21 192.168.20.254




Router Configuration:

Router>enable

Router# configure terminal

Router(config)# no ip dhcp excluded-address 192.168.20.13 192.168.20.254

Router(config)# ip dhcp excluded-address 192.168.20.21 192.168.20.254

Router(config)#ip dhcp pool LAN2_POOL

Router(dhcp-config)#network 192.168.20.0 255.255.255.0

Router(dhcp-config)#default-router 192.168.20.1

Router(dhcp-config)#dns-server 8.8.8.8

Router(dhcp-config)#exit





Now DHCP can assign:


192.168.20.10 - 192.168.20.20

Then on PC7:

Desktop → IP Configuration → DHCP

PC7 should receive: 192.168.20.13













<img width="1920" height="1080" alt="Screenshot (328)" src="https://github.com/user-attachments/assets/0c5d4ca8-cee2-485d-9396-5b5d85f5aed4" />






























## Step : 7


Renew IP ON the new PC7

ipconfig /release

ipconfig /renew

ipconfig

Expected after fix:

IP Address      : 192.168.20.13  ✅ IP assigned

Subnet Mask     : 255.255.255.0   ✅

Default Gateway : 192.168.20.1    ✅ gateway present













<img width="1920" height="1080" alt="Screenshot (336)" src="https://github.com/user-attachments/assets/b605dfcc-4fc3-4204-a94e-3bd8d375d8ff" />











































<img width="1920" height="1080" alt="Screenshot (327)" src="https://github.com/user-attachments/assets/e0ca1045-89d0-44f9-b004-25739d4ef921" />



































## Step : 8

## Verification-1





Router# show ip dhcp binding

Now shows multiple entries-new PC has an IP ✅





<img width="1920" height="1080" alt="Screenshot (330)" src="https://github.com/user-attachments/assets/4e5043df-c717-4096-a9e3-876e034ff56f" />































## Verification-2
























From new PC — Desktop — Command Prompt:

ping 192.168.20.1    ← ping router gateway

Expected: Reply from 192.168.20.1   ✅





<img width="1920" height="1080" alt="Screenshot (332)" src="https://github.com/user-attachments/assets/283e5f37-cd7a-47bf-97b2-4d913abb531c" />

































## 📋 Issue Summary



| Issue                            | Cause                      | Symptom                        | Fix                                              | Verified                        |
| -------------------------------- | -------------------------- | ------------------------------ | ------------------------------------------------ | :-----------------------------: |
| 1.    New PC cannot get IP        | DHCP Pool Exhausted        | Only new device fails          | Expanded Pool by reducing Excluded-Address Range | ipconfig /renew → IP   Assigned ✅ |
| 2.   Shows 0.0.0.0 or 169.254.x.x | No IPs available to assign | All existing devices work fine | -                                                |  Ping Successful ✅              |           |











Real World Ticket:

User Complaint:

I just connected my new laptop to the office network but I have no internet at all. All my colleagues sitting next to me are working fine.

Root Cause:

DHCP pool exhausted. All available IP addresses in the pool were already assigned to existing devices. The new laptop had no IP left to receive.

Resolution:

 Expanded the pool by reducing the excluded-address range. Ran ipconfig /renew on the new laptop. IP 192.168.20.13 assigned and internet access restored.












