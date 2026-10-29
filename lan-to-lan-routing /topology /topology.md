# 🖥️ Topology - LAN-to-LAN Routing Lab


 
 ## Step 1 - Open Cisco Packet Tracer and add devices to canvas
 




## 🔧 Devices Used

| Device | Model | Quantity | Purpose |
|---|---|---:|---|
| Router | Cisco 2911 | 1 | Routes traffic between two LANs |
| Switch | Cisco 2960 | 2 | Connects PCs within each LAN |
| PC | Generic PC | 6 | End-user devices — 3 per LAN |






## 🔌 Step 2 - Connect Cables

**Cable Type:** Copper Straight-Through for all connections.

| Source Device | Source Port | Destination Device | Destination Port |
|---|---|---|---|
| PC1 | FastEthernet0 | Switch 1 | FastEthernet0/1 |
| PC2 | FastEthernet0 | Switch 1 | FastEthernet0/2 |
| PC3 | FastEthernet0 | Switch 1 | FastEthernet0/3 |
| PC4 | FastEthernet0 | Switch 2 | FastEthernet0/4 |
| PC5 | FastEthernet0 | Switch 2 | FastEthernet0/5 |
| PC6 | FastEthernet0 | Switch 2 | FastEthernet0/6 |
| Switch 1 | GigabitEthernet0/1 | Router | GigabitEthernet0/0 |
| Switch 2 | GigabitEthernet0/1 | Router | GigabitEthernet0/1 |


---
<img width="1920" height="1080" alt="Screenshot (204)" src="https://github.com/user-attachments/assets/e7285ed4-07ca-492e-b8c2-48b0f8855e6a" />

























































**✅ Connection Status**

- 🟢 **Green indicators:** Connections are established.
- 🔴 **Red indicators:** Check the cable type and port selection, then reconnect if necessary.











## 🌐 Step 3 - Assign IP Addresses to All PCs

**Navigation:** Click each PC → **Desktop** tab → **IP Configuration** → **Static**

### 📋 IP Addressing Table

| PC IP Address | Subnet Mask | Default Gateway |
|---|---|---|
| `10.0.0.1` | `255.255.255.0` | `10.0.0.4` |
| `10.0.0.2` | `255.255.255.0` | `10.0.0.4` |
| `10.0.0.3` | `255.255.255.0` | `10.0.0.4` |
| `192.168.1.1` | `255.255.255.0` | `192.168.1.4` |
| `192.168.1.2` | `255.255.255.0` | `192.168.1.4` |
| `192.168.1.3` | `255.255.255.0` | `192.168.1.4` |

**📝 Note:** The default gateway is the router's IP address on the PC's local network.

- **LAN 1 - HR (PC1–PC3):** `10.0.0.4`
- **LAN 2 - Finance (PC4–PC6):** `192.168.1.4`










### 🖥️ PC1 IP Configuration - LAN 1 (HR)









<img width="1920" height="1080" alt="Screenshot (275)" src="https://github.com/user-attachments/assets/506a6d26-e8dc-4080-85f2-ef2cbb0e9f21" />





















































### 🖥️ PC4 IP Configuration - LAN 2 (Finance)












<img width="1920" height="1080" alt="Screenshot (278)" src="https://github.com/user-attachments/assets/c0903e53-0984-4e1d-8fa0-c44850e1edc0" />






































































