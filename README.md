# 📡 Cisco Packet Tracer – Static Routing Lab

## 📌 Devices Used

- 2 Routers (R1, R2) – Cisco 1941
- 2 Switches – Cisco 2960
- 2 PCs – PC1, PC2
- Ethernet Cables (Cross-over & Straight-through)

---

# 🔌 Physical Connections

## 1️⃣ Router to Router Connection

Connection:
R1 GigabitEthernet0/0  <---- Cross-over Cable ---->  R2 GigabitEthernet0/0

IP Addressing:

R1:
GigabitEthernet0/0 → 10.1.1.1 /24

R2:
GigabitEthernet0/0 → 10.1.1.2 /24

This network: 10.1.1.0/24 (Inter-router network)

---

## 2️⃣ R1 LAN Connection

R1 GigabitEthernet0/1  <---- Straight-through ---->  Switch S1
Switch S1 <---- Straight-through ----> PC1

IP Addressing:

R1:
GigabitEthernet0/1 → 192.168.1.1 /24

PC1:
IP Address → 192.168.1.10
Subnet Mask → 255.255.255.0
Default Gateway → 192.168.1.1

LAN Network: 192.168.1.0/24

---

## 3️⃣ R2 LAN Connection

R2 GigabitEthernet0/1  <---- Straight-through ---->  Switch S2
Switch S2 <---- Straight-through ----> PC2

IP Addressing:

R2:
GigabitEthernet0/1 → 192.168.2.1 /24

PC2:
IP Address → 192.168.2.10
Subnet Mask → 255.255.255.0
Default Gateway → 192.168.2.1

LAN Network: 192.168.2.0/24

---

# ⚙️ Router Configuration Commands

## 🔹 R1 Configuration


enable
configure terminal

interface g0/0
ip address 10.1.1.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

ip route 192.168.2.0 255.255.255.0 10.1.1.2
end
write memory

---

## 🔹 R2 Configuration


enable
configure terminal

interface g0/0
ip address 10.1.1.2 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

ip route 192.168.1.0 255.255.255.0 10.1.1.1
end
write memory
 Verification Commands

bash
show ip interface brief
show ip route
show ip route static

Connectivity Test

From PC1:

ping 192.168.2.10


If configuration is correct, ping should be successful.

---

# 🧠 How It Works

1. PC1 sends packet to its Default Gateway (192.168.1.1)
2. R1 checks static route
3. R1 forwards packet to 10.1.1.2 (R2)
4. R2 forwards packet to PC2
5. Reply returns via same path

---

# 🎯 Learning Outcome

- Understanding Static Routing
- Manual Route Configuration
- Router Interface Configuration
- End-to-End Connectivity Testing
- Basic Network Troubleshooting
