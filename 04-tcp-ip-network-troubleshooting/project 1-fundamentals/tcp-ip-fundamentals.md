
  ## 📖 TCP/IP Fundamentals



## 💡 What is TCP/IP?


 ## TCP- Transmission Control Protocol (TCP) is a connection-oriented protocol that ensures data is delivered reliably,
 
          in the correct order and without loss.


 ## IP- Internet Protocol (IP) is a network layer protocol responsible for addressing and routing data packets between devices on a network. 

        It assigns a unique IP address to each device, allowing data to be sent from a source device to the correct destination device.




 ##  🔄 The TCP/IP 4-Layer Model





  ## Layer 4-APPLICATION
  HTTP, HTTPS, DNS, FTP, SMTP, RDP

 ## Layer 3-TRANSPORT
  TCP (reliable) vs UDP (fast, no confirmation)

 ## Layer 2-INTERNET
  IP addressing and routing - IPv4, ICMP (ping)

 ## Layer 1-NETWORK ACCESS
  Ethernet cables, WiFi, MAC addresses, switches





 ## 🌐 IPv4 Basics


192.168.10.50

IPv4 uses 32 bits to represent an IP address.

8 + 8 + 8 + 8 = 32 bits

Three things every device needs:

1. IP Address     → unique identity
    
2. Subnet Mask    → defines local vs remote
 
3. Default Gateway → exit door to other networks



##  🏠 Public vs Private IP


PRIVATE - inside office or home:

10.0.0.0    – 10.255.255.255

172.16.0.0  – 172.31.255.255

192.168.0.0 – 192.168.255.255  ← most common

PUBLIC - assigned by ISP, unique worldwide



##  ⚙️ Static vs DHCP







| Type   | How Assigned          | Used For                   |
| ------ | --------------------- | -------------------------- |
| Static | Manually by admin     | Servers, printers, routers |
| DHCP   | Auto from DHCP server | PCs, laptops, phones       |



## 🚪 Default Gateway


C:\> ipconfig

Default Gateway: 192.168.10.1   ← your router

Without gateway → stuck on local network only

With gateway    → can reach internet and other LANs

Quick test:

ping 192.168.10.1

Reply ✅  → gateway up

Timeout ❌ → gateway problem







## 📋 Key Facts for Tier 1


| Item           | Detail                         |
| -------------- | ------------------------------ |
| Loopback       | 127.0.0.1 - always your own PC |
| APIPA          | 169.254.x.x -  DHCP failed     |
| Common Private | 192.168.x.x                    |
| Subnet /24     | 255.255.255.0                  |
| Ping 127.0.0.1 | Tests local TCP/IP stack       |
| Ping 8.8.8.8   | Tests internet bypassing DNS   |
