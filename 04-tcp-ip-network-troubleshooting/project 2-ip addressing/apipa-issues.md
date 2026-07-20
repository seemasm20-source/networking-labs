
  ## 🔴 IP Issue 4 — APIPA (169.254.x.x)


  ## 📋 Problem Summary
  
       PC shows an IP address starting with 169.254.x.x and has no internet or network access. The DHCP

      server is unavailable so the PC has self-assigned an APIPA address.




      .

   ## 🔍 Quick Overview


   169.254.x.x = APIPA address
   
            → = DHCP failed to respond
            
            →  = PC is isolated from network
            
           → = Cannot reach gateway or internet



    APIPA (Automatic Private IP Addressing) activates automatically on Windows when a PC set to DHCP cannot reach a DHCP server. The PC assigns itself

    an address from the 169.254.0.0/16 range. This address cannot communicate with any real network device it is a self-assigned fallback only.



       ## 🔧 Quick Verify

       C:\> ipconfig

       IP Address:      169.254.45.78   ← APIPA!
       
      Subnet Mask:     255.255.0.0
      
      Default Gateway:                 ← empty


     C:\> ping 192.168.10.1
     
     Request timed out ❌


  ## 🔧 Quick Fix




  C:\> ipconfig /release
  
  C:\> ipconfig /renew

If still APIPA:

→ Check cable is connected

→ Check DHCP server is running

→ Check switch port is active


 ## 🔗 Full Lab Documentation


 This scenario was fully documented in the

DHCP Configuration Portfolio including:

✅ Complete Packet Tracer lab setup
✅ Router DHCP configuration commands
✅ Fault simulation steps
✅ Step-by-step fix with CLI commands
✅ Verification screenshots
✅ Real-world help desk ticket
→ View full lab here:

[DHCP Portfolio — APIPA Issue](https://github.com/seemasm20-source/networking-labs/tree/main/dhcp-configuration)

