# MTCRE
 ## EOIP VPN:
```mermaid
graph LR
PC1{{PC-HO-side}}---|20.20.20.0/24|Mikrotik1((CCR-MIK-SITE-1<br>Ether-3-lan side :20.20.20.0/24))<-->|192.168.1.0/24|Mikrotik2((RB951-MKT-SITE-2))---PC{{PC}}
```
- Step 1: IP config in CCR-MKT 
- ![image](https://github.com/user-attachments/assets/8d1801df-5849-459f-9e50-bdb74b4728ee)
- Step 2: Ip config in RB951-MKT
- ![image](https://github.com/user-attachments/assets/02d1643e-9f6f-4062-8a51-d5ae52ca0370)
- Step 3: Create Interface for EoIP in CCR
  - Interface > EoIP > ADD > m
  - Remote IP. (192.168.1.2/24)
  - Self LAN interface MAC (internal)-eth3 mac address 
  -   - tunnel id = 1
  - ![image](https://github.com/user-attachments/assets/4346f62c-13a3-46f7-abaa-3e3527789bd1)

- Step 4: Bridge the Lan port and EoIP and Created the DHCP server in Bridge port.
   ![image](https://github.com/user-attachments/assets/7c9aff59-9542-42f6-afdc-aab79f387ad2)
   ![image](https://github.com/user-attachments/assets/b65fb113-ff26-41eb-890f-eeea2d733bae)
- Step 5:  

