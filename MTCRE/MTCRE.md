# MTCRE
 ## EOIP VPN:
```mermaid
graph LR
PC1{{PC-HO-side}}---|20.20.20.0/24|Mikrotik1((CCR-MIK-SITE-192.168.1.1/30<br>Ether-3-lan side :20.20.20.0/24))<-->|192.168.1.0/30|Mikrotik2((RB951-MKT-SITE-192.168.1.2/30))---PC{{PC}}
```
### Step 1: IP config in CCR-MKT 
- ![image](https://github.com/user-attachments/assets/8d1801df-5849-459f-9e50-bdb74b4728ee)
###Step 2: Ip config in RB951-MKT
- ![image](https://github.com/user-attachments/assets/02d1643e-9f6f-4062-8a51-d5ae52ca0370)
### Step 3: Create Interface for EoIP in CCR
  - Interface > EoIP > ADD > m
  - Remote IP. (192.168.1.1/24)
  - Self LAN interface MAC (internal)-eth3 mac address 
  -   - tunnel id = 1
  - ![image](https://github.com/user-attachments/assets/4346f62c-13a3-46f7-abaa-3e3527789bd1)

### Step 4: Bridge the Lan port and EoIP and Created the DHCP server in Bridge port.
   ![image](https://github.com/user-attachments/assets/7c9aff59-9542-42f6-afdc-aab79f387ad2)
   ![image](https://github.com/user-attachments/assets/b65fb113-ff26-41eb-890f-eeea2d733bae)
   ### Step 5: Do same in RB951 but do not create the DHCP server as the LAN will get ip from CCR.

---
---
---

  ## IPIP VPN:
```mermaid
graph LR
PC1{{PC-HO-side}}---|20.20.20.0/24|Mikrotik1((CCR-MIK-SITE-192.168.1.1/30<br>IPIPtunnel-10.10.10.1/30<br>Ether-3-lan side :20.20.20.0/24))<-->|P2P-192.168.1.0/30<br>IPIP tunnel: 10.10.10.0/30|Mikrotik2((RB951-MKT-SITE-192.168.1.2/30<br>IPIP tunnel-10.10.10.2/30<br>Lan network:30.30.30.0/24))---PC{{PC-Koshi-Branch}}
  ```
### Step 1 : Config the P2P and Lan network in both end.
### Step 2: Config IPIP Tunnel in CCR and RB951.
![image](https://github.com/user-attachments/assets/06ee644c-a931-4e29-81b9-21c250b8789d)

![image](https://github.com/user-attachments/assets/461ac7a8-2630-4ad3-9e77-ec58db91fe01)
### Step 3: Assign IP address to IPIP tunnel interface.
![image](https://github.com/user-attachments/assets/fb21cc3d-cfd4-41f7-8c59-4e647a493a7f)
![image](https://github.com/user-attachments/assets/4b46a991-147c-4bc1-b989-a9e6d749799b)
### Step 4: Add Static route in both router.
  ![image](https://github.com/user-attachments/assets/c349aa34-2c50-4fa9-90e6-190b31e9028e)
  ![image](https://github.com/user-attachments/assets/289c8164-1b94-4ad6-b526-fbd42b8bb368)




