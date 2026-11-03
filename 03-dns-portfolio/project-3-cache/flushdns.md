# 📋 DNS Cache: `ipconfig /flushdns`

## What is `ipconfig /flushdns`?

`ipconfig /flushdns` clears all entries from the local DNS Resolver Cache on a Windows computer. After the cache is cleared, Windows performs a fresh DNS lookup the next time a hostname is accessed.

---

## 💡 When to Run `flushdns`

- ✅ A website loads an old or wrong version
- ✅ A server moved to a new IP, but the old IP is still cached
- ✅ A DNS record was updated, but the PC ignores the update
- ✅ A new server hostname fails on some PCs

---

## 🔧 How to Run

### Step 1 - Open Command Prompt as Administrator

Press the **Windows key**, type `cmd`, then select **Run as administrator**.

### Step 2 - Generate a DNS lookup

```
C:\> ping google.com
```

This triggers a DNS lookup and caches the result.

### Step 3 - Confirm the record is in the cache

```
C:\> ipconfig /displaydns
```

The entry for `google.com` appears in the output.

### Step 4 - Flush the DNS cache

```
C:\> ipconfig /flushdns
```

Expected output: `Successfully flushed the DNS Resolver Cache.`

### Step 5 - Verify the cache is cleared

```
C:\> ipconfig /displaydns
```

The `google.com` entry is gone, so the cache was cleared.

---

## 🖼️ Screenshot









<img width="1920" height="1080" alt="Screenshot (362)" src="https://github.com/user-attachments/assets/546ae45b-79f3-4cf4-9bc2-2832cddaea18" />


