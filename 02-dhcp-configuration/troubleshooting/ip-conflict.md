
## Troubleshooting Issue-3


IP Address Conflict (Static vs DHCP)






## 📋 Problem Summary

PC2 manually assigned static IP 192.168.10.10 , same IP DHCP had already assigned to PC1. IP conflict caused intermittent failures for both devices.





## 🔧 Router Configuration



enable

configure terminal

interface gigabitEthernet0/0

ip address 192.168.10.1 255.255.255.0

no shutdown

exit

ip dhcp excluded-address 192.168.10.1 192.168.10.9

ip dhcp pool LAN1_POOL

network 192.168.10.0 255.255.255.0

default-router 192.168.10.1

dns-server 8.8.8.8

exit

end

write memory











## Step 1: Verify DHCP is Working

On PC1, navigate to:

Desktop → IP Configuration → DHCP

The PC should automatically receive an IP address from the DHCP server.

To verify the assigned network settings, open Command Prompt and run:

ipconfig /all
Expected Output
IP Address      : 192.168.10.10
Subnet Mask     : 255.255.255.0
Default Gateway : 192.168.10.1


Verification Confirm that:

The IP address belongs to the 192.168.10.0/24 network.
The subnet mask is 255.255.255.0.
The default gateway is 192.168.10.1.
The IP address was assigned automatically by DHCP.

This confirms that DHCP is functioning correctly before creating the troubleshooting scenario.





































<img width="1920" height="1080" alt="Screenshot (308)" src="https://github.com/user-attachments/assets/1e440650-ed4e-428e-a15d-a2825e345ece" />













































## Step 2: Create an IP Address Conflict

On **PC2**, navigate to:

**Desktop → IP Configuration → Static**

Configure the following settings:

```text
IP Address      : 192.168.10.10
Subnet Mask     : 255.255.255.0
Default Gateway : 192.168.10.1
DNS Server      : 8.8.8.8
```

### Conflict Scenario

At this point:

```text
PC1 = 192.168.10.10 (Assigned by DHCP)
PC2 = 192.168.10.10 (Configured Manually)
```

Both devices are using the same IP address, creating an **IP address conflict** on the network.
























































<img width="1920" height="1080" alt="Screenshot (309)" src="https://github.com/user-attachments/assets/25d3edb5-d296-45a8-b609-d85c1402607c" />



































## 🔎 Troubleshooting Process:





## User Report

Users report intermittent network connectivity. The connection drops randomly, and network access is unreliable.

---



### Check IP Configuration

On both PCs, open **Command Prompt** and run:

```bash
ipconfig /all
```

### Findings

```text
PC1 IPv4 Address : 192.168.10.10
PC2 IPv4 Address : 192.168.10.10
```

⚠️ Both devices are using the same IP address (`192.168.10.10`).

---






## Impact:

1.Intermittent connectivity

2.Communication failures

3.Access issues

4.Duplicate IP warnings in logs

5.Unpredictable network behaviour












## Resolution

To resolve the IP address conflict, change PC2 from a static IP configuration to DHCP.

Step 1: Configure PC2 to Use DHCP

Navigate to:

PC2 → Desktop → IP Configuration → DHCP

Step 2: Verify the New IP Address

The router's DHCP server assigns the next available IP address from the DHCP pool.

PC1 IP Address : 192.168.10.10
PC2 IP Address : 192.168.10.11

✅ Both devices now have unique IP addresses.

































<img width="1920" height="1080" alt="Screenshot (312)" src="https://github.com/user-attachments/assets/bca70cea-2ac7-4fe1-8988-856c53f5cf29" />



















<img width="1920" height="1080" alt="Screenshot (310)" src="https://github.com/user-attachments/assets/7b4f8d05-657c-4eb5-8a3f-4e8173b0b7e2" />





















































<img width="1920" height="1080" alt="Screenshot (311)" src="https://github.com/user-attachments/assets/234f5baa-1a8a-44fc-9373-7efc4727b74a" />












































## Verification

### Test Connectivity

From **PC2**, open **Command Prompt** and run:

```bash
ping 192.168.10.1
```

### Expected Result

```text
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
```

✅ Successful replies confirm connectivity to the default gateway.

---

### Verify IP Address Assignment

On both PCs, run:

```bash
ipconfig /all
```

### Results

```text
PC1 IPv4 Address : 192.168.10.10
PC2 IPv4 Address : 192.168.10.11
```

✅ Both devices now have unique IP addresses.

---

### Outcome

* IP address conflict resolved
* DHCP functioning correctly
* Network connectivity restored
* Devices can communicate without interruption
* Ping tests successful














<img width="1920" height="1080" alt="Screenshot (313)" src="https://github.com/user-attachments/assets/a77126ca-b10f-4724-81bf-7a4ca4a9ee9f" />















































<img width="1920" height="1080" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/b5db0da6-ee33-4eeb-abef-893a2cb84216" />
























## 📋 Issue Summary:





| Category         | Details                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Issue**        | PC1 and PC2 were both assigned the IP address **192.168.10.10**.                                                                    |
| **Cause**        | PC2 was manually configured with the same IP address that DHCP had already assigned to PC1.                                         |
| **Symptoms**     | Intermittent connectivity, random network drops and unreliable communication between devices.                                      |
| **Resolution**   | Changed PC2 from a static IP configuration to **DHCP**, allowing it to receive a unique IP address (**192.168.10.11**).             |
| **Verification** | Successfully pinged the default gateway (**192.168.10.1**) ✅ and confirmed unique IP addresses on both PCs using `ipconfig /all`   |






















User complaint

My connection randomly drops every few minutes no clear pattern.

Root cause

Duplicate IP conflict. PC2 manually set to same IP already leased to PC1. Network could not determine which device to reply to.

Resolution

Identified duplicate via ipconfig /all. Changed PC2 to DHCP. Router assigned unique IP 192.168.10.11. Connectivity stable andresolved.

