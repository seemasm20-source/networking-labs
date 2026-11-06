# 🗺️ Tracert Guide

---

## 💡 What is Tracert?

`tracert` shows every router (hop) your data passes through on its way to a destination. It helps show **where** along the path a problem occurs.

```text
C:\> tracert google.com

Tracing route to google.com [142.250.180.46]
over a maximum of 30 hops:

  1     1 ms     1 ms     1 ms   192.168.10.1      ← your router (default gateway)
  2     8 ms     9 ms     8 ms   10.0.0.1          ← ISP (Internet Service Provider)
  3    12 ms    11 ms    12 ms   172.16.5.1        ← ISP
  4    25 ms    24 ms    25 ms   142.250.180.46    ← destination

Trace complete.
```

> The addresses above are examples. Real traces show different addresses and often more hops.

---

## 📖 Reading the Output

| Column | Meaning |
|--------|---------|
| **Hop number** | The router or Layer 3 device in the path from your computer to the destination |
| **Three times (ms)** | Round-trip time of **three separate probe packets** sent to that hop. Used to spot latency and intermittent delays |
| **IP address / hostname** | The IP address or resolved hostname of the router that replied at that hop |

---

## ⚠️ Problem Output

```text
  1     1 ms     1 ms     1 ms   192.168.10.1     ✅
  2     8 ms     9 ms     8 ms   10.0.0.1         ✅
  3     *        *        *      Request timed out.   ← problem starts here
  4     *        *        *      Request timed out.
```

| Observation | Meaning |
|-------------|---------|
| Hops 1 and 2 reply | The local network and the first ISP router work |
| Hop 3 and every hop after it time out | Traffic stops at or after hop 3. The




## 💡 Next Step

→ Project 6 [[Ping & Tracert Troubleshooting](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%205-ping%26tracert.md)](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%206-real%20world%20tickets/no-internet-flowchart.md)
