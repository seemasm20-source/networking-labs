
## 🔴 IP Issue 2 - DHCP Lease Failure



## 📋 Problem Summary


## 📋 Problem Summary

## 📋 Problem Summary

A client was unable to obtain an IP address because the DHCP pool was missing from the router. 

Restoring the DHCP pool allowed the client to successfully receive a valid IP address.





## 🔍 What is a DHCP Lease Failure?



A DHCP lease failure occurs when a client device is unable to obtain or renew a valid IP address from a DHCP server. 

This can happen when the DHCP server is unavailable, the DHCP pool is missing or misconfigured, no IP addresses are 

available, or the client cannot communicate with the DHCP server.



## Steps to create simple lab in Cisco Packet Tracer:


##  Step :1 


Create the simple topology 

PC0          Switch0 
            
PC1           Router0


Use this network details:




| Device          | IP                |
| --------------- | ----------------- |
| Router G0/0     | `192.168.10.1/24` |
| PC0             | DHCP              |
| PC1             | DHCP              |
| DHCP pool       | `192.168.10.0/24` |
| Default gateway | `192.168.10.1`    |


## Step:2 



Connect the devices

Use Copper Straight-Through cables


PC0 FastEthernet0 → Switch Fa0/1

PC1 FastEthernet0 → Switch Fa0/2

Switch G0/1 → Router G0/0









<img width="1920" height="1080" alt="Screenshot (371)" src="https://github.com/user-attachments/assets/d7419454-700b-42c6-b98b-7b13863f2a12" />















































## Step 3: Configure the router interface


Open Router0 → CLI:-


enable

configure terminal

interface gigabitEthernet 0/0

ip address 192.168.10.1 255.255.255.0

no shutdown

exit













<img width="1074" height="398" alt="Screenshot (368)" src="https://github.com/user-attachments/assets/d7211ac9-99a4-4ef2-bcb2-e682acb54b8f" />































## Step 4: Configure DHCP

ip dhcp excluded-address 192.168.10.1 192.168.10.10

ip dhcp pool LAN_POOL

network 192.168.10.0 255.255.255.0

default-router 192.168.10.1

dns-server 8.8.8.8

exit


## Step 5: Get IP addresses on the PCs

On PC0 and PC1:

Desktop → IP Configuration → DHCP

They should receive addresses similar to:-


PC0 → 192.168.10.11

PC1 → 192.168.10.12






















<img width="1920" height="1080" alt="Screenshot (370)" src="https://github.com/user-attachments/assets/879a0992-0a32-4430-b9ac-40d7a8f255f0" />



















## Step 6: Create the DHCP failure in Router


enable

configure terminal

no ip dhcp pool LAN_POOL




 Note: Now the DHCP pool no longer exists. To properly demonstrate the failure, add a new PC (PC2) to the switch and set it to DHCP. 

 PC2 will request an address, but the router has no DHCP pool available to give it one.So it shows APIPA address.


















<img width="1920" height="1080" alt="Screenshot (372)" src="https://github.com/user-attachments/assets/97b0b372-c992-4c5b-b010-da36fe9d531c" />

































## Step 7: Fix the DHCP failure

Recreate the pool:-


configure terminal

ip dhcp pool LAN_POOL

network 192.168.10.0 255.255.255.0

default-router 192.168.10.1

dns-server 8.8.8.8

exit

On PC2, go to Desktop → IP Configuration and click DHCP again.















<img width="1920" height="1080" alt="Screenshot (373)" src="https://github.com/user-attachments/assets/ccaac241-07de-4df1-8e87-955d5e4773b4" />















































<img width="1920" height="1080" alt="Screenshot (374)" src="https://github.com/user-attachments/assets/e5a429a0-ae43-47b8-8a9b-0a2b755f0b36" />











































































































🔗 Full Lab Documentation

This scenario connects directly to DHCP pool exhaustion and APIPA scenarios documented in the

DHCP Configuration Portfolio including:


✅ Complete Packet Tracer lab setup

✅ DHCP pool configuration and exhaustion simulation

✅ Step-by-step fix with CLI commands

✅ Verification with show ip dhcp binding

✅ Real-world help desk ticket












→ View full lab here:  [DHCP Pool Exhaustion Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/dhcp-pool-exhaustion.md)
