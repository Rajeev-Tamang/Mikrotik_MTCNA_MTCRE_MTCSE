# MikroTik Certified Network Associate

## 1.How to upgrade RouterOS version 6 to 7.
- SYSTEM > PACKAGE > CHECK FOR UPDATE > CHANNEL: *UPGRADE* > DOWNLOAD & INSTALL.
- ***STABLE VERISON IS RECOMMENDED***
![image](https://github.com/user-attachments/assets/094e11a7-b45b-4f09-a2ed-23a03ea36f1b)


## 2.How to configure uplink in RouterOSv7 installed router.
- ```mermaid
  graph TB
  ISP-->Mikrotik
  Mikrotik-->LAN/PC/Station
  ```
  - Step 1 : IP address assign to WAN/LAN port.
![image](https://github.com/user-attachments/assets/15229ded-0518-48ee-bd4d-0e8b0ee14ad0)
![image](https://github.com/user-attachments/assets/4d017a40-6610-4a6e-b200-4a8d4a683777)
  - Step 2 : DHCP pool for lan users. (IP>DHCP_SERVER>DHCP_SETUP>....)
    ![image](https://github.com/user-attachments/assets/7c9e4204-4947-4b73-ab74-11275e0ad90c)
  - Step 3 : Routing for lan network
![image](https://github.com/user-attachments/assets/f7cd6643-3858-4498-98f3-8c4aedafa537)
  - Step 4: NAT ( IP > FIREWALL > NAT > ADD > CHAIN:srcnat > ACTION: masquerade.
  ![image](https://github.com/user-attachments/assets/bce36a07-0c95-4220-a29b-6e81dd7ecc2d)
![image](https://github.com/user-attachments/assets/7107d454-36a6-4519-86e1-c88d80d1cfda)


## 3. How to manage bandwidth using simple queue in RouterOS v7 router?
- QUEUES > ADD > SIMPLE QUEUES.
![image](https://github.com/user-attachments/assets/43e347c0-5c58-4061-99fb-6168ccad0fc8)

## 4. How to manage bandwidth using Per Connection  queue in RouterOS v7 router?
![image](https://github.com/user-attachments/assets/cd4c4a30-c45d-4042-8376-8f7f835ec6a4)
![image](https://github.com/user-attachments/assets/553b996e-c22c-479a-8578-1c1fdd926da8)
![image](https://github.com/user-attachments/assets/c62df88e-37bb-4a0a-b4ea-b99d56098eba)
![image](https://github.com/user-attachments/assets/cc23d4f6-f874-47b1-8157-a4956e152263)

## 5. How to create login user in RouterOS v7 router?
- SYSTEM > USER > ADD > ....
![image](https://github.com/user-attachments/assets/75bcc238-229f-43a9-baeb-acc9c00b63c7)

## 6. Backup & Restore Process in RouterOS v7 router?
 - FILES > BACKUP 
![image](https://github.com/user-attachments/assets/7bfb42f1-09f8-4775-806c-7fb05e2d3732)
- FILES > UPLOAD >...
- FILES > SELECT > RESTORE.

 ## 7.How to change the winbox default port number?
 - IP > services > winbox> edit.
![image](https://github.com/user-attachments/assets/0a8095c7-5b9d-477c-ac36-1b94349819b7)

## 8.How to configure wireless in routeros?
- Assign IP address to wlan interface.
- Create DHCP server for wireless client.
- wireless > security profile > add > name:xxx > mode: dynamic keys >
  ![image](https://github.com/user-attachments/assets/c43dc2d1-c1be-480b-adc1-512ed324353e)

## 9.How to block website.
![image](https://github.com/user-attachments/assets/736be60f-6e0f-43fb-a3c5-878aa4e0cc58)
![image](https://github.com/user-attachments/assets/e388190b-094a-4ca1-87c3-779fb1c2c221)
![image](https://github.com/user-attachments/assets/35cb1d42-b090-4820-b862-7af07c26a342)
![image](https://github.com/user-attachments/assets/a5582e1d-982a-451b-a122-7d1a29c46acd)

## 10.How to configure PPPoE server and client.
- Create ip pool for pppoe client.
![image](https://github.com/user-attachments/assets/7ece0922-6d3b-4b02-96c5-9be1fa18a336)
- Create PPP0E profile.
![image](https://github.com/user-attachments/assets/24f02e6a-71a1-4937-abbf-efc84ebe94bc)
- Create PPP0E secret(username & password).
 ![image](https://github.com/user-attachments/assets/3d4969f6-201a-4e99-8366-2d83e094d18d)
-Create PPPoE server bind it to physical interface or logical interface i.e vlan interface.
![image](https://github.com/user-attachments/assets/7c9309bb-a06d-46db-98be-2abc3aca1d49)

-- Client end
- PPP > ADD > PPPoE CLIENT>..
![image](https://github.com/user-attachments/assets/be7d33c9-b210-405c-8402-b7302631b6c2)

## 11. How to configure PPtP VPN server & client in routeros v7?
- Create PPTP profile.
- ![image](https://github.com/user-attachments/assets/4d5ba58b-dfe6-41f3-8023-66d97356be14)
- Create Secret(Username/Password)
- ![image](https://github.com/user-attachments/assets/ade83e9b-5b3b-41e3-aea5-c3dbe27513de)
- Enable PPTP Server.
- ![image](https://github.com/user-attachments/assets/be74d126-f456-476b-a8a9-f6eae5ea43fc)
- Client side config (Gateway is your mikrotik public ip)
- ![image](https://github.com/user-attachments/assets/add25159-c790-413d-bfae-31f39f0db1b7)

## 12. How to configure L2TP VPN server & client in routeros v7?
- create pool for l2tp client.
- ![image](https://github.com/user-attachments/assets/d29e3941-2c07-4a3a-b309-1f7e52b83125)
- Create profile
- ![image](https://github.com/user-attachments/assets/be4ddfca-fbb2-48d1-a6e3-ebfd2089f362)
- Create Secret
- ![image](https://github.com/user-attachments/assets/2f6b746e-3ca2-43df-a71e-a528a4f0ddce)
- Enable L2TP SERVER.
- ![image](https://github.com/user-attachments/assets/f95bd101-7ae0-4a81-a401-325d008de303)
- Client setup
- ![image](https://github.com/user-attachments/assets/69375703-bdb4-4ab9-ba61-c6bcf9375b77)
- ![image](https://github.com/user-attachments/assets/f73c8937-7b21-4f74-959d-ee2fd11acbe9)
- 

## 13.How to configure  static routing?
 ```mermaid
graph LR
PC{{PC-LAN}}---|20.20.20.0/24|MKT-1((MKT-1))---|192.168.50.0/30|MKT-2((MKT-2))---|30.30.30.0/24|PC2([PC-2_LAN])
  ```











