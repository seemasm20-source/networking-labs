
## 🔴 Service 4 - Firewall Connectivity Issues (user cannot access shared drive)


 ## 📋 Problem Summary



    User can ping devices but specific applications cannot connect. Issue appears after Windows update or security policy change.



    🔎 Verify

    Step 1: Verify network connectivity ping FILESERVER01 Reply ✅   ← server reachable


    Step 2: Attempt to access the shared folder

    :\> net use \\192.168.10.20\share
    
     System error 53 - network path not found 

     Port 445 (file sharing) likely blocked



     🔧 Fix


     Control Panel → Windows Defender Firewall
     
     → Advance setting → Inbound Rules→  File and Printer Sharing (SMB-IN)(Private) → Right click the rule → Enable Rule✅




























<img width="1920" height="1080" alt="Screenshot (411)" src="https://github.com/user-attachments/assets/e7d59b2f-42d2-48d7-8a46-87a4e94734fd" />


























































✅ Verification




C:\> net use \\192.168.10.20\share

Command completed successfully ✅

Now Open \\192.168.10.20\share in File Explorer

   

The shared folder opens successfully. The user confirms access has been restored.
