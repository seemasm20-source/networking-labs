# 🔴 Scenario 2 - Wrong DNS Server

[ Back to Project 2 README] → [README.md](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md)

---

## 📋 Problem Summary

A user cannot open any website or reach any server by name. Only this user is affected; colleagues on the same network work fine.

---



## 💡 What is a DNS Server?

A DNS server translates names (such as google.com) into IP addresses. If a PC points to a DNS server that does not exist or does not answer, every name lookup times out, even though the internet connection itself works.

---















## 🔧 Create the Problem

**Environment:** Windows 11, home network (Command Prompt, Windows network settings).

### Step 1 - Configure an invalid DNS server

1. Press **Windows + I** → **Network & Internet**
2. Open your active connection (Wi-Fi or Ethernet)
3. Click **Hardware properties**
4. Next to **DNS server assignment**, click **Edit** → choose **Manual** → turn on **IPv4**
5. Enter an invalid address:
   - Preferred DNS: `0.0.0.0`
   - Alternate DNS: `0.0.0.0`
6. Click **Save** and close all windows

**Screenshot: invalid DNS server 0.0.0.0 configured:**




<img width="1920" height="1080" alt="Screenshot (348)" src="https://github.com/user-attachments/assets/73eccb4a-c027-4a28-81dd-aef99e8149f8" />




---

### Step 2 - Disable IPv6

1. Press **Win + R**, type `ncpa.cpl`
2. Right-click the active network adapter → **Properties**
3. Untick **Internet Protocol Version 6 (TCP/IPv6)** → **OK**

> **Note:** I wanted to simulate a total DNS failure. After setting the dummy IPv4 DNS address my browsers could still resolve websites, because Windows was falling back to IPv6 DNS through my router. Disabling IPv6 forced Windows to rely on the IPv4 setting, so all DNS requests hit a dead end and the test environment was isolated.

---
















## 🔎 Verify the Problem

```text
C:\> ipconfig /all
DNS Servers . . . : 0.0.0.0        ← wrong address

C:\> nslookup google.com
*** Request to 0.0.0.0 timed-out

C:\> ping 8.8.8.8
Reply from 8.8.8.8                 ← the internet works

C:\> nslookup google.com 8.8.8.8
Address: 142.251.14.102            ← works with a valid DNS server
```

| Test | Result | Meaning |
|------|--------|---------|
| `ipconfig /all` | DNS server is 0.0.0.0 | The PC points to a DNS server that does not exist |
| `nslookup google.com` | Timed out | The DNS server does not answer |
| `ping 8.8.8.8` | Reply | Network connectivity is fine |
| `nslookup google.com 8.8.8.8` | Resolves | DNS works when a valid server is used |

> The internet works, but names do not resolve, so the fault is the DNS server setting.

**Screenshot: ipconfig /all showing DNS server 0.0.0.0:**






<img width="1920" height="1080" alt="Screenshot (347)" src="https://github.com/user-attachments/assets/4a7fa5f8-e00b-4f37-8be3-296a479db57b" />

























---



**Screenshot: nslookup timing out and ping 8.8.8.8 succeeding:**





<img width="1920" height="1080" alt="Screenshot (345)" src="https://github.com/user-attachments/assets/72a1d17b-8a24-4062-9224-7fbc4009de54" />





---




## 🔧 Fix

Set the DNS server back to a valid address:

1. **Windows + I** → **Network & Internet** → your connection → **Hardware properties**
2. Next to **DNS server assignment**, click **Edit**
3. Choose **Automatic (DHCP)**, or enter a valid server (for example the router at `192.168.0.1`)
4. Click **Save**

Re-enable IPv6 if you disabled it for the lab: **Win + R** → `ncpa.cpl` → adapter **Properties** → tick **Internet Protocol Version 6 (TCP/IPv6)** → **OK**.





**Screenshot: Assigning dhcp from manual to Automatic(dhcp):**



<img width="1920" height="1080" alt="Screenshot (381)" src="https://github.com/user-attachments/assets/3ed451af-ed43-40ef-9b87-f4d22f470f0c" />









<img width="1920" height="1080" alt="Screenshot (383)" src="https://github.com/user-attachments/assets/4ebd5af2-f62a-4eb1-b01c-67dcf99fb171" />

---












## ✅ Verification

### Verification 1 - DNS server

```text
C:\> ipconfig /all
```

The client now shows a valid DNS server.

**Screenshot: ipconfig /all showing a valid DNS server:**






<img width="1920" height="1080" alt="Screenshot (351)" src="https://github.com/user-attachments/assets/db2af8d5-867b-4b82-b196-c29790f42400" />






---



### Verification 2 - Name resolution

```text
C:\> nslookup google.com
```

The hostname resolves to an IP address.

**Screenshot: nslookup google.com returning an address:**







<img width="1920" height="497" alt="Screenshot (353)" src="https://github.com/user-attachments/assets/01fad31b-fdf2-458a-86ee-a36eb45261b5" />





---



### Verification 3 - Connectivity by name

```text
C:\> ping google.com
```

The name resolves and the client reaches the destination.

**Screenshot: ping google.com with replies:**






<img width="1920" height="694" alt="Screenshot (352)" src="https://github.com/user-attachments/assets/a7784c2f-53c0-4d85-aa59-8faf1a99b4e1" />










---



## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | Unable to open websites by name |
| **Cause** | Incorrect DNS server (0.0.0.0) configured on the client |
| **Symptom** | Websites fail by name; connectivity to IP addresses works |
| **Diagnose** | `ipconfig /all` showed 0.0.0.0, `nslookup google.com` timed out, `ping 8.8.8.8` worked |
| **Fix** | Set the DNS server back to a valid address in network settings |
| **Verified** | `nslookup google.com` and `ping google.com` succeed; websites load |

---

## 💡 Next Step

→ Scenario 3: [Internal vs. External DNS Resolution](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/internal-vs-external.md)


