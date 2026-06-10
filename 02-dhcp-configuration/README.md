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






                    ROUTER (Cisco 2911)
                  (DHCP server for both LANs)
                   /                        \
          Gi0/0                              Gi0/1
    IP: 192.168.10.1                   IP: 192.168.20.1
           |                                  |
    SWITCH 1 (2960)                    SWITCH 2 (2960)
   /      |       \                  /      |       \
 PC1     PC2      PC3               PC4     PC5    PC6






 ◄──────────── LAN 1 (HR) ────────────►

  Network : 192.168.10.0/24
  
  Gateway : 192.168.10.1
  
  Pool    : 192.168.10.10 – 192.168.10.50
  

◄──────────── LAN 2 (Finance) ───────►

  Network : 192.168.20.0/24
  
  Gateway : 192.168.20.1
  
  Pool    : 192.168.20.10 – 192.168.20.50


 




                   







📋 IP Address Plan

   Router Interfaces — manually configured


| Interface    | IP address   | Subnetmask    | Role              |
| ------------ | :----------: | :-----------: | ----------------- |
| Router Gi0/0 | 192.168.10.1 | 255.255.255.0 | Gateway for LAN 1 |
| Router Gi0/1 | 192.168.20.1 | 255.255.255.0 | Gateway for LAN 2 |
                                                              
                                                              





















                    ROUTER (Cisco 2911)
                   /                   \
          Gi0/0                         Gi0/1
    IP: 10.0.0.4                  IP: 192.168.1.4
           |                             |
    SWITCH 1 (2960)              SWITCH 2 (2960)
   /      |      \              /      |      \
 PC1     PC2     PC3          PC1     PC2     PC3

 ◄────── LAN 1 (HR) ────────► ◄──── LAN 2 (Finance) ────►
  Network: 10.0.0.0/24          Network: 192.168.1.0/24
  Gateway: 10.0.0.4             Gateway: 192.168.1.4






                
◄──────────── LAN 1 (HR) ────────────►
  Network : 192.168.10.0/24
  Gateway : 192.168.10.1
  Pool    : 192.168.10.10 – 192.168.10.50

◄──────────── LAN 2 (Finance) ───────►
  Network : 192.168.20.0/24
  Gateway : 192.168.20.1
  Pool    : 192.168.20.10 – 192.168.20.50

