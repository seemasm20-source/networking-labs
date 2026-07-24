

## 🔴 Connectivity 2 - Ping IP Works, Name Fails











## 📋 Problem Summary

   User can ping 8.8.8.8 successfully but cannot open any website by name. Internet connectivity is working - DNS is not.





## Step 1: Test IP Connectivity

ping 8.8.8.8

 The ping was successful, confirming that basic IP connectivity is working and the device can reach external networks.




## Step 2: Test Name Resolution

ping google.com

The domain-name ping failed, indicating a possible DNS name-resolution issue that requires further investigation.











<img width="1920" height="1080" alt="Screenshot (386)" src="https://github.com/user-attachments/assets/57434cd4-770c-4aa2-a914-60a411a28287" />










## 🔎 Verify




## Step 3: Check DNS Configuration 


C:\> ipconfig /all 


Check the DNS server address configured on the active network adapter to verify whether the correct DNS server is being used.







## Step 4: Test DNS Directly

nslookup google.com

The DNS lookup timed out, indicating that the configured DNS server may be unreachable or incorrectly configured.

















<img width="1920" height="1080" alt="Screenshot (387)" src="https://github.com/user-attachments/assets/1a068f32-bb39-460b-9c5a-8acc27c60bb9" />







































 ## 🔧 Fix

Configure a valid DNS server or restore the network adapter's DNS settings to Automatic (DHCP).

 Network Settings → IPv4 → DNS:

Preferred: 8.8.8.8

Alternate:  8.8.4.4


check out DNS Portfolio for full troubleshooting guide → [DNS Troubleshooting Labs](https://github.com/seemasm20-source/networking-labs/tree/main/03-dns-portfolio/project-2-troubleshooting)





## ✅ Verification

Successful name resolution confirms that DNS functionality has been restored.


C:\> nslookup google.com

Address: 192.168.0.156  ✅

C:\> ping google.com      Reply ✅







<img width="1920" height="1080" alt="Screenshot (388)" src="https://github.com/user-attachments/assets/741125db-9596-4245-ba88-d0f25a159263" />



