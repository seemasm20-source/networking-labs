
  ## 📋  Connectivity 4 - Intermittent Connectivity

[ Back to Project README] → [README.md](./README.md)

---

> **Lab Note:** Intermittent faults come and go, so they are hard to reproduce on demand. The outputs below are illustrative and show how packet loss and delay appear in each tool. Actual values vary with the environment.

## 📋 Problem Summary

The connection works, then drops randomly. Downloads are unreliable and video calls drop. There is no clear pattern.

---

## 💡 What is Intermittent Connectivity?

Intermittent connectivity means the connection is not fully down but is unstable. Some packets are lost or delayed, which breaks real-time traffic such as video calls first.

| Symptom | Detail |
|---------|--------|
| Random drops | The connection works, then fails, then returns |
| Unreliable downloads | Downloads stall or restart |
| Video calls drop | Real-time traffic is affected first |

**Common causes:**

- Weak Wi-Fi signal or interference
- Bandwidth-heavy applications running in the background
- An outdated or faulty wireless adapter driver
- A faulty cable or switch port
- A problem on the ISP side

> **First step:** find where the loss starts, on the PC, on the local network or beyond it.

---

## 🔎 Verify the Problem

| Test | Command | What it shows |
|------|---------|---------------|
| 1. Check the configuration | `ipconfig /all` | The adapter has a valid IP address, subnet mask, default gateway and DNS servers |
| 2. Test the gateway continuously | `ping -t 192.168.10.1` | Packet loss or delay on the local network |
| 3. Trace the path | `pathping google.com` | Where along the route packets are lost |

### Test 1 - Check the configuration

```text
C:\> ipconfig /all
```

Verify that the active adapter has a valid IP address, subnet mask, default gateway and DNS servers, and that its status is connected, before looking for packet loss.

### Test 2 - Ping the gateway continuously

```text
C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Request timed out.                         ← packet dropped
Reply from 192.168.10.1: bytes=32 time=2ms TTL=64
Request timed out.                         ← dropped again
Reply from 192.168.10.1: bytes=32 time=45ms TTL=64   ← delay spike
^C

Ping statistics for 192.168.10.1:
    Packets: Sent = 20, Received = 18, Lost = 2 (10% loss)
```

Press **Ctrl + C** to stop. Lost packets and delay spikes on the gateway ping point to the local network, such as Wi-Fi, a cable or a switch port.

### Test 3 - Trace the path with pathping

```text
C:\> pathping google.com
```

```text
Tracing route to google.com [142.250.74.14]
over a maximum of 30 hops:
  0  LAPTOP-MN70JUKE
  1  Default Gateway
  2  ISP Router
  3  ISP Core Router
  4  * * *

Computing statistics for 75 seconds...
            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct
  0                           0/100 = 0%
  1    6ms     0/100 =   0%   0/100 = 0%
  2   14ms     0/100 =   0%   0/100 = 0%
  3   ---    100/100 = 100%   0/100 = 0%

Trace complete.
```

`pathping` combines route tracing with packet loss analysis, so it shows whether the loss starts on the local network, inside the ISP network or further along the path.

> In this sample, hop 3 shows 100% loss in the left column but 0% in the "This Node/Link" column. That usually means the router does not answer these test packets, but still forwards traffic, so it is not a real fault.

---

## 🔧 Fix

- Improve the Wi-Fi signal by moving closer to the router or using the 5 GHz band
- Pause bandwidth-heavy applications (Windows Update, OneDrive, cloud sync)
- Update the wireless network adapter driver
- Check the cable and switch port if the PC is wired
- If packet loss continues beyond the local network, contact the ISP with the `pathping` results

---

## ✅ Verification

```text
C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
^C

Ping statistics for 192.168.10.1:
    Packets: Sent = 30, Received = 30, Lost = 0 (0% loss)
```

All 30 packets reached the gateway with 0% loss, so the connection is stable.

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | The connection drops randomly |
| **Cause** | Weak Wi-Fi signal, background bandwidth use or an outdated adapter driver |
| **Symptom** | Unreliable downloads and dropped video calls with no clear pattern |
| **Diagnose** | `ping -t` to the gateway showed packet loss; `pathping` located where loss starts |
| **Fix** | Improved the Wi-Fi signal, paused heavy applications and updated the adapter driver |
| **Verified** | Continuous ping to the gateway showed 0% packet loss |

---

## 💡 Next Step

→ [Connectivity 5](./connectivity-5.md)
