

## 🔴 Scenario 2 - Slow Network Performance


##  📋 Problem Summary

   Internet or network very slow. Pages take long to load. Video calls dropping. Issue intermittent - no clear pattern.





   ## 🔎 Step 1 - Measure ping to gateway
   
     C:\> ping -t 192.168.10.1
     
      time=1ms
      
     time=45ms   ← spike!
     
     time=1ms
     
    time=120ms  ← spike again!
    
   → Intermittent high latency on local network
   
   → Likely cable or switch issue








   ## 🔎 Step 2 - pathping for detailed analysis
     
     C:\> pathping google.com

       Hop 1 (gateway):  0% loss ✅
       
       Hop 2 (ISP):      0% loss ✅
       
      Hop 3:           25% loss  ← problem HERE
      
      → ISP network congestion
      
      → Escalate to ISP with pathping output









  ## 🔧 Fix
      
Local packet loss → replace cable, different port

ISP issue         → restart router, contact ISP

Bandwidth hogs    → Task Manager → Resource Monitor

WiFi              → move closer, switch to 5GHz









## ✅ Verification

C:\> ping -t 192.168.10.1

time=1ms  time=1ms  time=1ms

Packets: Sent=50 Received=50  Lost=0 (0% loss) ✅











➡️ **Related Lab:** > **Related Troubleshooting Lab:** See **[Intermittent Connectivity](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/intermittent-connectivity.md)** for diagnosing packet loss, high latency, and unstable network connections. :contentReference[oaicite:0]{index=0}
