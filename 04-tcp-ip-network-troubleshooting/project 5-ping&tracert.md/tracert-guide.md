

## 🗺️ Tracert Guide

## 💡 What is Tracert?

   Shows every router your data passes through. Reveals exactly WHERE in the path a problem occurs.

  C:\> tracert google.com

 * 1     1 ms     1 ms     1 ms   192.168.10.1   → your router(Default Gateway)

 * 2     8 ms     9 ms     8 ms   10.0.0.1       → (Internet Service Provider-ISP)

 * 3    12 ms    11 ms    12 ms   172.16.5.1    →  (Internet Service Provider)

 * 4    25 ms    24 ms    25 ms   142.250.180.46  → (Internet)





## 📖 Reading Output



  
| Column                    | Meaning                                                                                                                    |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Hop Number**            | Identifies the router or Layer 3 device in the path from your computer to the destination.                                 |
| **Three Times (ms)**      | The round-trip time for **three separate probe packets** sent to that hop. Used to detect latency and intermittent delays. |
| **IP Address / Hostname** | The IP address or resolved hostname of the router that responded at that hop.                                              |


  ##  Problem Output
   
*  1     1 ms     1 ms     1 ms   192.168.10.1  ✅
  
*  2     8 ms     9 ms     8 ms   10.0.0.1      ✅
  
*  3     *        *        *      Request timed out  ← PROBLEM
  
*  4     *        *        *      Request timed out

→ Problem at hop 3 - ISP or upstream issue

→ Escalate with this tracert output as evidence



## ⭐ Asterisk (* * *)

Stars with subsequent hops responding → firewall blocking tracert (normal)

Stars where all subsequent hops also * → that hop is down (problem)
