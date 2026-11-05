

# 🔴 Connectivity 1 - Cannot Ping Gateway

[ Back to Project README] → [README.md](./README.md)

---


## 📋 Problem Summary

A PC has a valid IP address but cannot ping its default gateway. It has no internet access and cannot reach anything outside its local subnet. In this lab the cause was an incorrect default gateway configured manually on the PC.

---


## 💡 What is a Wrong Default Gateway?

The default gateway is the router address a PC uses to leave its local network. If the gateway setting points to an address that does not exist, the PC still works inside its own subnet, but traffic to other networks and the internet fails.

| Symptom | Detail |
|---------|--------|
| Valid IP address and subnet mask | The PC is configured, not APIPA |
| Gateway ping fails | The configured gateway does not reply |
| No internet access | Traffic cannot leave the local subnet |

> **First check:** compare the gateway shown by `ipconfig /all` with the correct router address.


**Screenshot: `ipconfig /all` showing the correct gateway:**












<img width="1920" height="1080" alt="Screenshot (375)" src="https://github.com/user-attachments/assets/d24f9bf3-829f-46db-a825-90bd50bdebba" />









---


## 🧪 Create the Problem

### Step 1 - Record the working configuration

```text
C:\> ipconfig /all
```

Note the working IPv4 address, subnet mask, default gateway and DHCP status. The correct default gateway in this lab is `192.168.0.1`.





### Step 2 - Configure a wrong gateway

Change the IPv4 configuration from **Automatic (DHCP)** to **Manual**:

**Settings → Network & internet → Wi-Fi → Hardware properties → IP assignment → Edit → Manual → IPv4 On**

| Setting | Value |
|---------|-------|
| IP Address | `192.168.0.156` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.0.250` ❌ |
| DNS Server | `8.8.8.8` |







<img width="1920" height="1080" alt="Screenshot (382)" src="https://github.com/user-attachments/assets/c7b11112-9a6d-4b9f-856f-ae186abdd2ab" />











---





## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Check the configuration | `ipconfig /all` | Gateway `192.168.0.250` | The gateway differs from the working one |
| 2. Ping the configured gateway | `ping 192.168.0.250` | Request timed out | The gateway address does not exist on the network |
| 3. Compare with the working gateway | Configured `192.168.0.250` ❌ vs correct `192.168.0.1` ✅ | Mismatch | The incorrect gateway is the root cause |

**Screenshot: `ipconfig /all` showing the wrong gateway:**

<img width="1920" height="1080" alt="Screenshot (380)" src="https://github.com/user-attachments/assets/8fe9ed6a-8179-4227-a6e8-4270b44944be" />






---


**Screenshot: ping to the wrong gateway fails:**

<img width="1920" height="1080" alt="Screenshot (380)" src="https://github.com/user-attachments/assets/5b54ee95-006d-48f5-a625-08d3bbab229a" />



---









## 🔧 Fix

Set the IPv4 configuration back to **Automatic (DHCP)**, so the PC receives the correct address, subnet mask and gateway:

**Settings → Network & internet → Wi-Fi → Hardware properties → IP assignment → Edit → Automatic (DHCP)**

If the PC uses a static address on purpose, change the default gateway to the correct value (`192.168.0.1`) instead.

---






## ✅ Verification

| Command | Result | Meaning |
|---------|--------|---------|
| `ipconfig /all` | Gateway `192.168.0.1` | Correct configuration |
| `ping 192.168.0.1` | Reply ✅ | The gateway is reachable |
| `ping 8.8.8.8` | Reply ✅ | The internet is reachable |
| `ping google.com` | Reply ✅ | DNS and internet are working |



**Screenshot: correct configuration and gateway ping:**

<img width="1920" height="1080" alt="Screenshot (384)" src="https://github.com/user-attachments/assets/d4eeb9d7-956b-429d-8175-014cfa2158e9" />

**Screenshot: internet and DNS pings succeed:**

<img width="1920" height="1080" alt="Screenshot (385)" src="https://github.com/user-attachments/assets/1c44fb1d-0e87-4d23-89cc-ddf421fc8d32" />




---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | PC cannot ping its default gateway and has no internet |
| **Cause** | Incorrect default gateway (`192.168.0.250` instead of `192.168.0.1`) configured manually |
| **Symptom** | Valid IP address, gateway ping fails, no access outside the local subnet |
| **Diagnose** | `ipconfig /all` showed the wrong gateway; `ping 192.168.0.250` timed out |
| **Fix** | Set the IPv4 configuration back to Automatic (DHCP) |
| **Verified** | Gateway `192.168.0.1` replied; `8.8.8.8` and `google.com` replied |

---



## 💡 Next Step

→ [Connectivity 2](./connectivity-2.md)




































