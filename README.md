# 🖧 OSPF Network Lab


---

## 1) OSPF implemented
**OSPF (Open Shortest Path First)** is a **link-state routing protocol**. Routers exchange **Link-State Advertisements (LSAs)** to describe their interfaces and neighbors. Each router builds the same **link-state database (LSDB)** and runs **Dijkstra’s SPF algorithm** to calculate the shortest paths.  

- **Areas:** The network is split into **Area 0 (backbone)** and **Areas 1, 2, 3**.  
- **Backbone:** Area 0 is mandatory in multi-area OSPF; all other areas must connect to it.  
- **ABR (Area Border Router):** Routers between Area 0 and other areas. They maintain LSDBs for multiple areas and summarize LSAs.  
- **Result:** With OSPF, all PCs across all areas can connect through shortest, loop-free paths.

---

## 2) IPs are assigned automatically by DHCP
A central DHCP service assigns IP addresses, subnet masks, default gateways, and DNS servers automatically (here DNS is not provided). This avoids manual configuration errors and speeds up network deployment.

---

## 3) VLANs help bind DHCP to the right interfaces
The network uses **VLANs** to separate devices into logical subnets. Each VLAN:  
- Maps to one **IP subnet**  
- Has a dedicated **DHCP pool**  
- Gets routed by its **default gateway** on the router/L3 switch  

This ensures clients receive the correct addressing information for their VLAN.

---

## 4) IEEE 802.1Q encapsulation
Links between switches and routers are configured as **802.1Q trunks**. This tagging ensures:  
- VLAN frames keep their identity end-to-end  
- DHCP requests from each VLAN are forwarded correctly  
- Inter-VLAN routing works without confusion  

---

## 5) Purpose of this project
- ✅ Show how OSPF backbone & ABRs provide scalable multi-area routing  
- ✅ Demonstrate automatic IP allocation with DHCP per VLAN  
- ✅ Use IEEE 802.1Q encapsulation to carry VLAN traffic across trunks  
- ✅ Prove that **all PCs in the lab can connect with each other** through correct routing

---

## 📊 Router Configuration Table

| Router  | Interface   | IP Address       | Area |
|---------|-------------|------------------|------|
| Router 00 | Se0/1/0 | 192.186.10.11 | 0 |
| Router 00 | G0/0/0  | 192.186.100.1 | 0 |
| Router 0  | Se0/1/0 | 192.172.10.10 | 0 |
| Router 0  | Se0/1/1 | 192.172.30.10 | 0 |
| Router 0  | Se0/2/0 | 192.172.20.10 | 0 |
| Router 0  | Se0/2/1 | 192.186.10.10 | 0 |
| Router 0  | G0/0/0  | 172.28.100.1   | 0 |
| Router 10 | Se0/1/0 | 192.172.10.11 | 0 |
| Router 10 | Se0/1/1 | 192.168.11.11 | 1 |
| Router 10 | Se0/2/0 | 192.168.114.11 | 1 |
| Router 10 | G0/0/0  | 172.28.10.1   | 1 |
| Router 11 | Se0/1/0 | 192.168.11.10 | 1 |
| Router 11 | Se0/1/1 | 192.168.12.10 | 1 |
| Router 11 | G0/0/0  | 172.28.11.1   | 1 |
| Router 12 | Se0/1/0 | 192.168.13.11 | 1 |
| Router 12 | Se0/1/1 | 192.168.12.11 | 1 |
| Router 12 | G0/0/0  | 172.28.12.1   | 1 |
| Router 13 | Se0/1/0 | 192.168.14.10 | 1 |
| Router 13 | Se0/1/1 | 192.168.13.10 | 1 |
| Router 13 | Se0/2/0 | 192.168.115.10 | 1 |
| Router 13 | G0/0/0  | 172.28.13.1   | 1 |
| Router 14 | Se0/1/0 | 192.168.114.12 | 1 |
| Router 14 | Se0/1/1 | 192.168.14.12 | 1 |
| Router 14 | G0/0/0  | 172.28.14.1   | 1 |
| Router 15 | Se0/1/0 | 192.168.115.11 | 1 |
| Router 15 | G0/0/0  | 172.28.15.1   | 1 |
| Router 20 | Se0/1/0 | 192.172.20.11 | 0 |
| Router 20 | Se0/1/1 | 192.168.21.11 | 2 |
| Router 20 | Se0/2/0 | 192.168.225.11 | 2 |
| Router 21 | Se0/1/0 | 192.168.21.10 | 2 |
| Router 21 | Se0/1/1 | 192.168.22.10 | 2 |
| Router 21 | G0/0/0  | 172.28.21.1   | 2 |
| Router 22 | Se0/1/0 | 192.168.22.11 | 2 |
| Router 22 | Se0/1/1 | 192.168.23.11 | 2 |
| Router 22 | G0/0/0  | 172.28.221.1  | 2 |
| Router 22 | G0/0/1  | 172.28.222.1  | 2 |
| Router 23 | Se0/1/0 | 192.168.23.10 | 2 |
| Router 23 | Se0/1/1 | 192.168.24.10 | 2 |
| Router 23 | G0/0/0  | 172.28.23.1   | 2 |
| Router 24 | Se0/1/0 | 192.168.25.11 | 2 |
| Router 24 | Se0/1/1 | 192.168.24.11 | 2 |
| Router 24 | G0/0/0  | 172.28.24.1   | 2 |
| Router 25 | Se0/1/0 | 192.168.225.12 | 2 |
| Router 25 | Se0/1/1 | 192.168.25.12 | 2 |
| Router 25 | G0/0/0  | 172.28.25.1   | 2 |
| Router 30 | Se0/1/0 | 192.172.30.11 | 0 |
| Router 30 | Se0/1/1 | 192.168.33.11 | 3 |
| Router 30 | Se0/2/0 | 192.168.131.11 | 3 |
| Router 30 | G0/0/0  | 172.28.30.1   | 3 |
| Router 31 | Se0/1/0 | 192.168.31.10 | 3 |
| Router 31 | Se0/1/1 | 192.168.131.10 | 3 |
| Router 31 | G0/0/0  | 172.28.31.1   | 3 |
| Router 32 | Se0/1/0 | 192.168.32.11 | 3 |
| Router 32 | Se0/1/1 | 192.168.31.11 | 3 |
| Router 32 | G0/0/1  | 172.28.36.1   | 3 |
| Router 32 | G0/0/0  | 172.28.37.1   | 3 |
| Router 33 | Se0/1/0 | 192.168.33.10 | 3 |
| Router 33 | Se0/1/1 | 192.168.32.10 | 3 |
| Router 33 | G0/0/1  | 172.28.38.1   | 3 |
| Router 33 | G0/0/0  | 172.28.39.1   | 3 |

---

## 🔧 Verification Commands
```bash
show ip ospf neighbor
show ip ospf database
show ip route ospf
show vlan brief
show interfaces trunk
show ip dhcp binding
show ip dhcp pool
ping <remote-PC>
traceroute <remote-PC>
