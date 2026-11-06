# 🔴 Scenario 2 - Slow Network Performance

[ Back to Project README] → [README.md](./README.md)

---

> **Lab Note:** Slow-network faults come and go, so they are hard to reproduce on demand. The outputs below are illustrative and show how delay and packet loss appear in each tool. Actual values vary with the environment.

## 📋 Problem Summary

The internet or network is very slow. Pages take a long time to load and video calls drop. The issue is intermittent, with no clear pattern.

---

## 💡 What is a Slow Network Problem?

A slow network usually means high latency (delay), packet loss or too little bandwidth. The connection is not fully down, so the first job is to find **where** the delay or loss starts: on the PC, on the local network or beyond it.

| Possible cause | Where it shows up |
|----------------|-------------------|
| Faulty cable, switch port or weak Wi-Fi | Delay or loss on the ping to the gateway |
| Background applications using bandwidth | Slow speeds with a normal gateway ping |
| ISP congestion or a fault | Loss appears at a hop beyond your router |

> **First check:** ping the gateway, then trace the path. If the gateway is fine, the problem is beyond the local network.

---

## 🔎 Verify the Problem

| Test | Command | What it shows |
|------|---------|---------------|
| 1. Measure ping to the gateway | `ping -t 192.168.10.1` | Delay spikes or packet loss on the local network |
| 2. Analyse the path | `pathping google.com` | Where along the route packets are lost |

### Test 1 - Measure ping to the gateway

```text
C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: time=1ms
Reply from 192.168.10.1: time=45ms     ← spike
Reply from 192.168.10.1: time=1ms
Reply from 192.168.10.1: time=120ms    ← spike again
^C
```

Press **Ctrl + C** to stop. Repeated spikes on the gateway ping point to a problem on the local network, such as a cable, switch port, Wi-Fi signal or a busy PC.

### Test 2 - Analyse the path with pathping

```text
C:\> pathping google.com

Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct
  1   2ms     0/100 =  0%     0/100 =  0%   ← gateway
  2  10ms     0/100 =  0%     0/100 =  0%   ← ISP
  3  35ms    25/100 = 25%    25/100 = 25%   ← loss starts here
```

Hop 1 (gateway) and hop 2 (ISP) show 0% loss, and hop 3 shows 25%. This points to congestion or a fault on the ISP network.

> Loss at one hop is a real fault only if it continues at the hops after it. If later hops show 0% loss, the router is just slow to answer test packets and traffic is not affected.

---

## 🔧 Fix

| Cause | Fix |
|-------|-----|
| Local packet loss | Replace the cable or use a different switch port |
| Weak Wi-Fi | Move closer to the router or switch to the 5 GHz band |
| Bandwidth-heavy applications | Check **Task Manager → Performance → Open Resource Monitor** and pause the heaviest applications |
| ISP issue | Restart the router, then contact the ISP with the `pathping` output |

---

## ✅ Verification

```text
C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: time=1ms
Reply from 192.168.10.1: time=1ms
Reply from 192.168.10.1: time=1ms
^C

Ping statistics for 192.168.10.1:
    Packets: Sent = 50, Received = 50, Lost = 0 (0% loss)
```

All 50 packets reached the gateway with 0% loss and steady times, so the connection is stable.

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | The network is slow and video calls drop |
| **Cause** | Local delay or packet loss, or congestion on the ISP network |
| **Symptom** | Slow pages and dropped calls with no clear pattern |
| **Diagnose** | `ping -t` showed delay spikes; `pathping` showed 25% loss at hop 3 |
| **Fix** | Replaced the cable or port, improved Wi-Fi, paused heavy applications, or contacted the ISP |
| **Verified** | Continuous ping to the gateway showed 0% packet loss |

---

## 💡 Next Step

→ Project 5 [Ping & Tracert Troubleshooting](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%205-ping%26tracert.md)
