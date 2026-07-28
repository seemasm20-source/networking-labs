        Service 1 - DNS Resolution Issues


     ## 📋 Problem Summary

          User cannot open websites by name. Internet connectivity works when tested by IP.






   ##  🔎 Quick Diagnostic

        C:\> ping 8.8.8.8      Reply ✅   ← internet works
   
        C:\> ping google.com   Fails ❌   ← DNS problem

       C:\> nslookup google.com   Timed out ❌   ← DNS server not responding






   ## 🔧 Quick Fix

   Preferred DNS: 8.8.8.8
   
   Alternate DNS: 8.8.4.4





  ## 🔧 Full Reference
    
Complete DNS troubleshooting with 5 scenarios is documented in the DNS Portfolio → project2-troubleshooting

https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/wrong-dns-server.md?utm_source=chatgpt.com
