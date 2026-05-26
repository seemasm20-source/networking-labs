🖥️ Network Topology



<img width="1920" height="1080" alt="Screenshot (204)" src="https://github.com/user-attachments/assets/e7285ed4-07ca-492e-b8c2-48b0f8855e6a" />




























🔧 Devices Used

| Device Model      | Quantity | Purpose                       |
| ----------------- | -------: | ----------------------------- |
| Router Cisco 2911 | 1        | Routes Traffic Between 2 LANs |
| Switch Cisco 2960 | 2        | Connects PCs Within Each LAN  |
| PC Generic PC     | 6        | End User Devices — 3 Per LAN  |















Step 2 — Connect Cables
Cable type: Copper Straight-Through for all connections







| Device   | Interface       | Switch   | Connected Device   | Connected Interface |
| -------- | --------------- | -------- | ------------------ | ------------------- |
| PC1      | FastEthernet0   | Switch 1 | PC2                | FastEthernet0       |
| PC3      | FastEthernet0   | Switch 1 | PC4                | FastEthernet0       |
| PC5      | FastEthernet0   | Switch 2 | PC6                | FastEthernet0       |
| Switch 1 | GigabitEthernet | Router   | GigabitEthernet0/0 | Switch 2            |
| Switch 2 | GigabitEthernet | Router   | GigabitEthernet0/1 | Switch 1            |











✅ All cable dots turn green = connected correctly
🔴 Red dot = wrong cable or wrong port — delete and redo











Step 3 — Assign IPs to All PCs
Click each PC → Desktop tab → IP Configuration → Static









| PC IP       | Subnet Mask   | Default Gateway |
| ----------- | ------------- | --------------: |
| 10.0.0.1    | 255.255.255.0 | 10.0.0.4        |
| 10.0.0.2    | 255.255.255.0 | 10.0.0.4        |
| 10.0.0.3    | 255.255.255.0 | 10.0.0.4        |
| 192.168.1.1 | 255.255.255.0 | 192.168.1.4     |
| 192.168.1.2 | 255.255.255.0 | 192.168.1.4     |
| 192.168.1.3 | 255.255.255.0 | 192.168.1.4     |






Note: Default gateway is the router's IP on that PC's side.
LAN 1 PCs (PC1–PC3) → gateway 10.0.0.4
LAN 2 PCs (PC4–PC6) → gateway 192.168.1.4










PC1 IP configuration — LAN 1 (HR):









<img width="1920" height="1080" alt="Screenshot (275)" src="https://github.com/user-attachments/assets/506a6d26-e8dc-4080-85f2-ef2cbb0e9f21" />















<img width="1920" height="1080" alt="Screenshot (276)" src="https://github.com/user-attachments/assets/a5ce7926-3d53-4857-80e0-0689c30ec177" />












<img width="1920" height="1080" alt="Screenshot (277)" src="https://github.com/user-attachments/assets/5c49260e-42e7-41a8-89df-91cb1fa34f2c" />
























PC4 IP configuration — LAN 2 (Finance):












<img width="1920" height="1080" alt="Screenshot (278)" src="https://github.com/user-attachments/assets/c0903e53-0984-4e1d-8fa0-c44850e1edc0" />

























<img width="1920" height="1080" alt="Screenshot (279)" src="https://github.com/user-attachments/assets/3013682b-9651-4f5a-b7ea-9cf93adfe31c" />


















<img width="1920" height="1080" alt="Screenshot (280)" src="https://github.com/user-attachments/assets/d0771b32-fbf0-4045-ac89-d1966645867b" />

























