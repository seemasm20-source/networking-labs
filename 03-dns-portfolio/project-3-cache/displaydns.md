


# 🔍 DNS Cache: ipconfig /displaydns

  [← Back to DNS Portfolio README](../README.md)

 ---



## 💡 What is ipconfig /displaydns?

`ipconfig /displaydns` displays all DNS records currently stored in the local DNS cache.

The cached entries contain recently resolved domain names and their IP addresses. They let Windows resolve names faster without contacting the DNS server for every request.

## ▶️ How to Run

```cmd
C:\> ipconfig /displaydns
```

---

## 📖 Reading the Output

```text
google.com
----------------------------------------
Record Name . . . . . : google.com
Record Type . . . . . : 1
Time To Live  . . . . : 127
Data Length . . . . . : 4
Section . . . . . . . : Answer
A (Host) Record . . . : 142.251.14.113
```

### 📋 Understanding the Output

| Field | Description |
|---|---|
| **Record Name** | The domain name stored in the local DNS cache (for example, `www.google.com`). |
| **Record Type** | The DNS record type. **1 = A (Host) record**, which maps a hostname to an IPv4 address. |
| **Time To Live (TTL)** | The remaining time, in seconds, that Windows keeps the record in the cache before a new lookup is required. |
| **Data Length** | The size of the record data in bytes. An **A record** is **4 bytes** (an IPv4 address is 32 bits). |
| **Section** | The part of the DNS response the record belongs to. **Answer** means it directly answers the query. |
| **A (Host) Record** | The IPv4 address associated with the hostname. |

### 📸 Screenshot - `ipconfig /displaydns` Output showing cached records


<img width="1920" height="1080" alt="Screenshot (361)" src="https://github.com/user-attachments/assets/2c16ac45-de85-46d2-bdc6-792ede5ce867" />









---




























 **Note:** Many websites, including Google, support both **IPv4** and **IPv6**. When Windows performs a DNS lookup for these websites, 
 
 it may cache both **A (IPv4)** and **AAAA (IPv6)** records if they are returned by the DNS server. 
 
 As a result, `ipconfig /displaydns` can display both record types in the local DNS cache.










    
