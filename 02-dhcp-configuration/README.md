networking-labs / dhcp-configuration / README.md

🌐 DHCP Server Configuration using Cisco Router



Portfolio: Networking Labs-DHCP Configuration

Tool: Cisco Packet Tracer

Author: Seema

Date: May 2026


📌 Objective


This project simulates two office departments HR (LAN 1) and Finance (LAN 2) where a Cisco 2911 router acts as a DHCP server.

Instead of manually assigning IPs, the router automatically assigns IP addresses, subnet masks, default gateways and DNS to all devices.





💡 What is DHCP? 


DHCP stands for Dynamic Host Configuration Protocol.

It is a network management protocol used to automatically assign IP addresses and other crucial 

communication settings (like subnet masks, default gateways, and DNS servers) to devices on a network, allowing them to communicate efficiently


Without DHCP                   With DHCP


IT person manually types IP  → Router assigns IP automatically


Time consuming                  → Instant


Easy to make mistakes           → Consistent and accurate




How It Works:


When a device connects to a network, the protocol follows a four-step sequence known by the acronym DORA:


 ⇒Discover: The device broadcasts a message to find a DHCP server.
 
 
 ⇒Offer: The DHCP server receives the request and offers an available IP address to the device.
 
 
 ⇒Request: The device broadcasts a request to accept the offered IP address.
 
 
 ⇒Acknowledge: The server sends an acknowledgment confirming the assignment and granting a "lease" to use the address for a specific period
 









🖥️ Network Topology






                   ```text
                ROUTER (Cisco 2911)
          DHCP Server for Both LANs
                   /        \
              Gi0/0          Gi0/1
      192.168.10.1      192.168.20.1
             |                |
        SWITCH 1          SWITCH 2
       (Cisco 2960)      (Cisco 2960)
         /  |  \           /  |  \
       PC1 PC2 PC3      PC4 PC5 PC6
```


  
.


| LAN Name        | Network         | Gateway      | IP Pool                       |
| --------------- | --------------- | ------------ | ----------------------------- |
| LAN 1 (HR)      | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.10 – 192.168.10.50 |
| LAN 2 (Finance) | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.10 – 192.168.20.50 |
 




                   







📋 IP Address Plan

   Router Interfaces manually configured


| Interface    | IP address   | Subnetmask    | Role                      |
| ------------ | ----------      | -----------| -----------------         |
| Router Gi0/0 | 192.168.10.1 | 255.255.255.0 | Default Gateway for LAN 1 |
| Router Gi0/1 | 192.168.20.1 | 255.255.255.0 | Default Gateway for LAN 2 |



Device IP Addressing Information



| Device        | LAN            | IP Assignment Method | Gateway      |
|--------------|----------------|---------------------|----------------|
| PC1          | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC2          | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC3 (Laptop) | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC4          | LAN 2 (Finance)| DHCP                | 192.168.20.1   |
| PC5          | LAN 2 (Finance)| DHCP                | 192.168.20.1   |
| PC6 (Laptop) | LAN 2 (Finance)| DHCP                | 192.168.20.1   |

                                                           
                                                              
🔧 Devices Used


| Device | Model          | Quantity | Purpose                                                |
| ------ | -------------- | -------- | ------------------------------------------------------ |
| Router | Cisco 2911     | 1        | Routes traffic between LANs and provides DHCP services |
| Switch | Cisco 2960     | 2        | Connects end devices within each LAN                   |
| PC     | Generic PC     | 4        | End-user workstations                                  |
| Laptop | Generic Laptop | 2        | PC3 (LAN 1) and PC6 (LAN 2)                            |






 🛠️ Technologies Used



| Technology          | Purpose                                               |
| ------------------- | ----------------------------------------------------- |
| Cisco Packet Tracer | Network simulation and testing environment            |
| Cisco 2911 Router   | Inter-LAN routing and DHCP services                   |
| Cisco 2960 Switch   | Layer 2 switching within each LAN                     |
| DHCP Protocol       | Automatic IP address assignment                       |
| Cisco IOS CLI       | Router configuration and management                   |




🔴 Issues Encountered

Real problems faced during this lab full details

in the troubleshooting folder.




| Issue                           | Cause                                                     | File                                    |
| ------------------------------- | --------------------------------------------------------- | --------------------------------------- |
| PCs showing 169.254.x.x — APIPA | DHCP service disabled                                     | apipa-issues.md                |
| DHCP Pool Exhaustion            | DHCP scope exhausted, no available IP addresses remaining | dhcp-pool-exhaustion.md |
| Duplicate IP address conflict   | Static IP clashes with DHCP                               | ip-address-conflict.md  |







📂 Project Files





| Section              | Description                                               |
| -------------------- | :-------------------------------------------------------: |
| Topology             | Network diagram, IP table and build steps                 |
| DHCP Config          | Full router CLI commands with explanation                 |
| APIPA Issue          | 169.254.x.x — DHCP service disabled                       |
| DHCP Pool Exhaustion | DHCP scope exhausted, no available IP addresses remaining |
| IP Conflicts         | Static IP clashing with DHCP lease                        |












                   
