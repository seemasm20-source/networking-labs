## ⚙️ Router Configuration

### 📌 Overview

The Cisco 2911 router is configured with two interfaces: one connected to HR (LAN 1) and the other connected to Finance (LAN 2).

 All commands are entered through the **CLI** tab inside Cisco Packet Tracer.

### 🖥️ How to Open Router CLI

1. Click the router on your Packet Tracer canvas.
2. Select the **CLI** tab at the top of the window.
3. Press **Enter** if prompted to continue.
4. The router command prompt will appear










| Prompt             | Level          | How to get there         |
| ------------------ | -------------- | ------------------------ |
| Router>            | User Mode      | Default when CLI opens   |
| Router#            | Privileged     | type: enable             |
| Router(config)#    | Global Config  | type: configure terminal |
| Router(config-if)# | Interface Mode | type: interface Gi0/0    |





















## ⚙️ Router Configuration Commands

```text
Router> enable
Router# configure terminal

! --- LAN 1 interface (HR Department) ---
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 10.0.0.4 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- LAN 2 interface (Finance Department) ---
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip address 192.168.1.4 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- Save configuration ---
Router# write memory
```

















---
> **📝 Note:** The default gateway on each PC must match the router interface IP address for its LAN.
>
> - **LAN 1 (HR):** `10.0.0.4`
> - **LAN 2 (Finance):** `192.168.1.4`
---




























































<img width="1920" height="1080" alt="Screenshot (285)" src="https://github.com/user-attachments/assets/add73d0c-ec56-4ce3-a9b5-d977226fa777" />















































---

## 📘 What Each CLI Command Does

| Command | What It Does |
|---|---|
| `enable` | Enters privileged EXEC mode, providing access to advanced commands. |
| `configure terminal` | Enters global configuration mode to make configuration changes. |
| `interface GigabitEthernet0/0` | Selects the router interface connected to LAN 1 (HR). |
| `ip address 10.0.0.4 255.255.255.0` | Assigns the IP address and subnet mask to the interface. |
| `no shutdown` | Enables the interface, which may be administratively disabled by default. |
| `exit` | Exits the current configuration mode and returns to the previous level. |
| `write memory` | Saves the running configuration to startup configuration so it persists after a restart. |












## ✅ Verification Commands

After completing the router configuration, run the following command to verify the interface status and IP addresses:

```text
Router# show ip interface brief
```










**Check that both router interfaces are active:**



**Expected Output:**

| Interface | IP-Address | OK | Status | Protocol |
|---|---|:---:|---|:---:|
| GigabitEthernet0/0 | 10.0.0.4 | YES | up | up |
| GigabitEthernet0/1 | 192.168.1.4 | YES | up | up |






























**Screenshot - show ip interface brief confirming both interfaces are up:**






































<img width="1920" height="1080" alt="Screenshot (266)" src="https://github.com/user-attachments/assets/fe55cb39-a690-4ab5-abd3-757c52c09234" />

































































---
## 🔎 Ping Test - Cross-LAN Connectivity

     From PC1 (10.0.0.1) open:

     Desktop → Command Prompt

     Then ping each device:

































| IP Address  | Device | Same LAN? | Expected Reply |
| ----------- | ------ | :-------: | -------------- |
| 10.0.0.2    | PC2    | Yes       | Reply ✅        |
| 10.0.0.3    | PC3    | Yes       | Reply ✅        |
| 192.168.1.1 | PC4    | No        | Reply ✅        |
| 192.168.1.2 | PC5    | No        | Reply ✅        |
| 192.168.1.3 | PC6    | No        | Reply ✅        |










































### 📸 Screenshot - Successful Cross-LAN Ping
---

































<img width="1920" height="1080" alt="Screenshot (257)" src="https://github.com/user-attachments/assets/dba27950-bec4-4a49-8926-0cca5fcb699c" />
















---
<img width="1920" height="1080" alt="Screenshot (258)" src="https://github.com/user-attachments/assets/1e6423c5-1b04-4b84-a4d7-d33c8ab03e54" />






















---
<img width="1920" height="1080" alt="Screenshot (284)" src="https://github.com/user-attachments/assets/26cd15b3-72d0-4050-9d28-329dcf9e042b" />



























 ---
<img width="1920" height="1080" alt="Screenshot (259)" src="https://github.com/user-attachments/assets/ee4b3825-3902-4cc3-b8c7-4e5fb818bc07" />


























 ---
<img width="1920" height="1080" alt="Screenshot (260)" src="https://github.com/user-attachments/assets/6d7933b4-a667-42e4-9fde-8549134c6086" />








