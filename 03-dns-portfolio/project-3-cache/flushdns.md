
## 📋Cache- ipconfig /flushdns


What is ipconfig/ flushdns?

ipconfig /flushdns clears all entries from the local DNS Resolver Cache on a Windows computer. After the cache is cleared, Windows performs a fresh DNS lookup the next time a 

hostname is accessed.


## 💡 When to Run flushdns

✅ Website loads old/wrong version

✅ Server moved to new IP- old IP still cached

✅ DNS record updated but PC ignores update

✅ New server hostname fails on some PCs








## 🔧 How to Run :


## Step 1 - Open CMD as Administrator

Windows key → type cmd → Run as Administrator



## Step 2 - C:\> ping google.com

Generates a DNS lookup and caches the result.

## Step 3 - Run command
C:\> ipconfig /displaydns

Confirms the DNS record is in the cache



## Step 4 - Run command

C:\> ipconfig /flushdns

Successfully flushed the DNS Resolver Cache



## Step 5 - Run command

C:\> ipconfig /displaydns

nothing shown cache is empty













































<img width="1920" height="1080" alt="Screenshot (362)" src="https://github.com/user-attachments/assets/546ae45b-79f3-4cf4-9bc2-2832cddaea18" />


