# MTCSE
## 1. How to we upgrade router OS and firmware verion?
- System > Check for updates > Download and install.
![Router OS Upgrade](https://github.com/Rajeev-Tamang/MTCSE/blob/main/RouterOS%20Upgrade.jpg)

## 2. How to upgrade router board firmware?
- System > RouterBoard > Upgrade > Reboot for change.
![Router Board Firmware Upgrade](https://github.com/Rajeev-Tamang/MTCSE/blob/main/router%20Board%20firmware%20upgradejpg.jpg)

## 3. How do we control access to mikrotik router?

**Note**: ***Removing the defualt admin user after creating new user with full access or setting strong password for admin user is highly recomended.***
 
- Ip address of mikrotik router is: 172.16.210.210/24
- Allowed address for user rajeev is : 172.16.210.239/24
![Allowed user and ip address](https://github.com/Rajeev-Tamang/MTCSE/blob/main/allowed%20user%20and%20ip%20address.jpg)

![IP address before](https://github.com/Rajeev-Tamang/MTCSE/blob/main/ip%20address%20before.jpg)

![Login Failed](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Login%20Failed.jpg)
- Since ip address is 172.16.210.233/24 , it is not accesible. Lets Change the ip address and try again.
![Allowed Ip address](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Login%20allowed.jpg)
-Now User: rajeev with ip address 172.16.210.239 is allowed to access.

## 4. How do we disable and Change service port?
- IP > Services > Select > Enable ✅	/ Disable ❌
![IP Service port](https://github.com/Rajeev-Tamang/MTCSE/blob/main/service%20port%20enable%20disable%20change.jpg)

***Note: If you do not use certain services , its recommended to disable it***
  ***Changing service port is also highly recommeded , default winbox port is 8291**

## 5. How do we disable MAC access.?
- Tools > Mac server > Mac telnet / Mac winbox / Mac Ping.
![Mac ping](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20ping%20%20server.jpg)

![Mac Telnet](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20telnet%20server.jpg)

![Mac winbox](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20winbox%20server.jpg)

***Note: In production network is not a good pratice to enable mac access, mac ping mac telnet.***

## 6. How do we diasble neighbor discovery?
- IP > Neighbor > Discovery Setting >  Interface > None > Apply.
![Neigbor discovery Disable](https://github.com/Rajeev-Tamang/MTCSE/blob/main/neighbor%20disable.jpg)

***Note: We see neighbor in winbox table, it is highly recommended to disable the Neighbor discovery***


## 7. How do we disable ping request from firewall?
- IP > Firewall > ADD > Chain = Input > source address=0.0.0.0/0 > Protocol= ICMP > Action = drop > Apply > Ok

![Firewall rule 1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%201.jpg)

![Firewall rule 2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%202.jpg)

![Firewall rule 3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%203.jpg)


## 8. How to use Forward Chain?
- Forward chain ->passing through our mikrotik router. Packet arrives in mikrotik and it determine what to do with the packet that is passing through 
  mikrotik to outer network.

- Suppose you want to block the users from accessing youtube.com.

- IP > Firewall > Layer 7 Protocols > ADD > Name:Youtube > Regexp: www.Youtube.com > 
  Apply > OK

![layer 7 protocol define for blocking youtube](https://github.com/Rajeev-Tamang/MTCSE/blob/main/layer7protocol.jpg)
- IP > Firewall > Fiter rules > ADD > Chain = Forward > Src.address = 172.16.210.0/24 > Advance > Layer 7 Protocols = Youtube > Action = Drop > Apply > OK .

![Block youtube.com Forward Chain](https://github.com/Rajeev-Tamang/MTCSE/blob/main/forwardchain%20youtube%20block1.jpg)

![Block youtube.com](https://github.com/Rajeev-Tamang/MTCSE/blob/main/forward%20chain%20youtube%20block%202.jpg)

![Block youtube.com 3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/forward%20chain%20youtube%20block%203.jpg)


## 9. How do we use Output Chain?

- Output chain processess packets originatin from the router itself.

- Suppose we want to Block the icmp packet form our mikrotik to cloudflare dns 1.1.1.1 
  then, 
- IP > Firewall > Filter Rules > ADD > Chain = Output > Protocol = ICMP > out.interface 
  = Ether1 > Action = drop > Apply > OK.

![output chain](https://github.com/Rajeev-Tamang/MTCSE/blob/main/outputchain%201.jpg)

![Output chain2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/output%20chain%202.jpg)

![Output Chain3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/output%20chain3.jpg)


## 10. Source NAT

- IP > Firewall > NAT > ADD > Chain = Srcnat > Action = masquerade > Apply > OK.


## 11. How can i redirect traffic from one port to another?

- Destination NAT or dstant. It is most commonly used to make hosts on a private 
  netwrok to be accessible from the internet.

- But we can use it to redirect it to another port, suppose traffic is coming for 80 port we can redirect it to 8080 ports.

- IP > webproxy >  Enable > Apply >  OK
  
- IP > Webproxy > Access > Add > DST = rajeev.com > Action = allow/deny > Apply > ok

![Web proxy](https://github.com/Rajeev-Tamang/MTCSE/blob/main/webproxy1.jpg)

![dstnat1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/dstnat1.jpg)

![dstnat2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/dstnat2.jpg)

- Now when client access the ***rajeev.com:80*** it will be redirected to port 8080 and will be determine either allow or deny the request.

## 12. Why and how to use mangle routing?
- Mangle marking routing is used for policy-based routing. It allows you to route 
  specfic packet based on criteria beyong just their destionation IP address.

- Lets consider we have two department HR with ip pool of 192.168.10.0/25 and Account 
 with ip pool of 192.168.10.128/25. Also we have two isp uplink , Vianet with ip 
 172.16.1.1/24 and Dish Home with ip 172.16.2.1/24. we want HR traffic via vianet and 
 Account traffic via DishHome.

![IPaddress](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle1.jpg)
- IP > Firewall > Mangle > Add > Chain = Prerouting > src.address = 192.168.10.0/25 
 Action = mark routing > New routing mark = HR Department .

![MAngle1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle2.jpg)
![](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle3.jpg)

- IP > Firewall > Mangle > Add > Chain = Prerouting > src.address = 192.168.10.128/25 
 Action = mark routing > New routing mark = Account Department .

![Mangle Account](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle4.jpg)
![Mgl account](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle5.jpg)

- IP > routes > Add > Gateway > ether2 > Routing mark = HR Department > Apply > OK
![](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Mangle6.jpg)

- IP > routes > Add > Gateway > ether3 > Routing mark = Account Department > Apply > OK
![](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mangle7.jpg)


## 13. How can we group IP address  into list for easier rule management?
- we can use addresslist if we want efficient and organized firewall rule  management, 
  especailly when dealing with numbers of ip address.

  - IP > Firewall > address list > Add > Name = xxxx > address = 1.1.1.1 / x.x.x.x > 
     Apply > OK

  - Repeat with other ip but same addresslist.
 
  ![addresslist](https://github.com/Rajeev-Tamang/MTCSE/blob/main/addresslist1.jpg)

  - Ip > Firewall > Filter rules > Add > Chain = input > advance > Src.address list > address-list-ip >  Action = Drop > Apply > oK. 

![addresslist2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/addresslist2.jpg)
![addresslist3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/addresslist3.jpg) 
![addresslist4](https://github.com/Rajeev-Tamang/MTCSE/blob/main/addresslist4.jpg)
![addresslist5](https://github.com/Rajeev-Tamang/MTCSE/blob/main/addresslist5.jpg)

## 14. How can we view and Manage the active connections on Mikrotik router.?
- IP > Firewall > Connection > 
- If we see that tracking is set to no, then we will not be seeing any active 
 connection which may also result in internet no working.
![Connection Tracking](https://github.com/Rajeev-Tamang/MTCSE/blob/main/ConnectionTracking.jpg)

## 15. How do we use Mikrotik Firewall raw?

- Mikrotik routers include a feature called the "raw" firewall, which is used to hanel 
  packet at a lower level compared to the traditional firewall (filter rules). The raw 
  tables allows you to bypass connection tracking, which can be beneficial for 
  performance and certain security.

## 16. How do we configure PPTP server & client?

- Step 1: Enable PPPTP server.
   - PPP > PPTPSERVER > ENABLE > APPLY > OK
 ![PPPTP SERVER ENABLE](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP1.jpg)
- Step 2: Creat pool 
    - IP > POOL > ADD > NAME = XXXX > ADDRESS = 192.168.200.2 - 192.168.200.254> APPLY  
       > OK 
![IP POOOL](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP3.jpg)

- Step 3: Create profile
   - PPP > PROFILES > ADD > NAME = XXXX > LOCAL ADDRESS = 192.168.200.1 > REMOTE  
      ADDRESS = PPPTP-IP-POOL > LIMITS >  RATE LIMIT (RX/TX): 2M/2M > APPLY > OK
![PPTP PROFILE](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP4.jpg)
![PPTP PROFILE 2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP5.jpg)

- Step 4: Create user & password.
    - PPP > SECRETS > ADD > NAME =rajeev > Password = 12345678 > SERVICE = PPTP > PROFILE > PPTP PROFILE 2M > APPLY OK

 - Step 5: PPTP SERVER BINDING.
    - PPP > INTERFACE > PPTP SERVER BINDING > APPLY OK.
![PPTP SERVER BINDING](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP7.jpg)
      
- Step 6: Check from client PC.
![PPTP_VPN](https://github.com/Rajeev-Tamang/MTCSE/blob/main/PPPTP8.jpg)


## 17. How to configure L2TP vpn?
 - The process is similar to PPTP. This one will be your task, try yourself.

## 18. How to Configure SSTP VPN ? 

## 20.How to configure OpenVpn Client & Server ?

- STEP 1 : Create CA.
       - SYSTEM > CERTIFICATES > ADD > NAME = XXXX > COMMAN NAME = XXXX > KEY USAGE > 
         KEY CRT.SIGN & CRL SIGN > APPPLY > SIGN > CA CRL HOST = PUBLIC IP/WAN IP OF 
         MIKROTIK > APPLY > OK
![OPENVPN1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn1.jpg)
![OPENVPN2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn2.jpg)

- STEP 2: CREATE SERVER CERTIFICATE.
       - SYSTEM >  CERTIFICATE > ADD > NAME = XXX > COMMON NAME = XXXX > KEY USAGE = 
         DIGITAL SIGNATURE , KEY ENCIPHERMENT & TLS SERVER > APPLY > SIGN > CA = CA > 
         APPLY > GENERAL > TRUST = ENABLE > APPLY > OK 
![OPENVPN3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn3.jpg)
![OPENVPN4](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn4.jpg)

-STEP 3: CREATE CLIENT CERTIFICATE.
        - SYSTEM >  CERTIFICATE > ADD > NAME = XXX > COMMON NAME = XXXX > KEY USAGE = 
          TLS CLIENT > APPLY > SIGN > CA = CA > 
          APPLY > GENERAL > TRUST = ENABLE > APPLY > OK 

![OPENVPN5](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn5.jpg)
![OPENVPN6](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn6.jpg)

***EXPORT THE CA AND CLIENT CERTIFICATED WITH PASSWORD.***

- STEP 4 : CREATE IP POOL FOR VPN CLIENT
     - IP > POOL > ADD > NAME = OPENVPN-POOL > ADDRESS = 172.16.112.2-172.16.112.254
![OPENVPN7](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn7.jpg)

- STEP 5: CREATE OPENVPN PROFILE.
  - PPP > PROFILE > ADD > NAME = OVPN > LOCAL ADDRESS = 172.16.124.1 > REMOTE- 
    ADDRESS = OPENVPN-POOL
![OPENVPN8](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn8.jpg)

- STEP 6 : CREATE USERNAME AND PASSWORD OF VPN USER.
    - PPP > SECREATS > ADD > NAME = TEST > PASSWORD = 12345678910 > SERVICE = OVPN > 
      PROFLE = OVPN > APPLY > OK .
![](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn9.jpg)

- STEP 7 : OPENVPN SERVER SETUP.
     - PPP > OPENVPN  SERVER > ADD > NAME = XXXX > DEFAULT PROFILE = OVPN > CERTIFICATE > SERVER > REQUIRED CLIENT CERTIFICATE = YES > REDIRECT GATEWAY > DEF1 > APPLY > OK 
    ![](https://github.com/Rajeev-Tamang/MTCSE/blob/main/openvpn10.jpg)

- *Export.opvn from openvpn server tab , it is stored in files of mikrotik and download it to your 
   local machine.*
 - *Allow ovpn port 1194, IP > FIREWALL > ADD > CHAIN = INPUT > PROTOCOL > TCP > DST.PORT = 1194 > 
    ACTION = ACCEPT > APPLY > OK*
 - *SRC.NAT WITH MASQURADE*
 - *ALL SET CONFIG IN IMPORT THE DOWNLOADED .OVPN FILE IN , CLIETN END DEVICE*

## 21.How to Configure Wiregaurd VPN Server & Client? 
- WireGuard® is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and 
  more useful than IPsec while avoiding massive headaches. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a 
  general-purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the 
  Linux kernel, it is now cross-platform (Windows, macOS, BSD, iOS, Android) and widely deployable.

- Wireguard > Add > Name = xxxx > Interface = wireguard1 > Apply > OK.
-  *A Public key will be generated that will be needed in client end*

![WireGuard1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd1.jpg)

- Interface > Address > Add > Address = 192.168.1.1/24 > Apply > OK
 ![Wiregaurd2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd2.jpg)

-  Wireguard > Peer > Name = xxxxx > Interface = wireguard1 > Publickey = client end  
    public key > Allowed Address = Ip address of Client end (example: 192.168.1.2/32)  
    >Apply > OK
![Wireguard3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurdpeer.jpg)

- IP > FIREWALL > FILTER RULES > CHAIN = INPUT > PROTOCOL = UDP > DST.PORT = 13231 > ACTION =  ACCEPT > APPLY > OK
- IP > FIREWALL > FILTER RULES > CHAIN > INPUT > SRC.ADDRESS=192.168.1.0/24 > ACTION = ACCEPT > APPLY > OK 

![WIRE4](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd4.jpg)
![WIRE5](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd5.jpg)

- Now , lets setup in client mobile device.
![client1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd7.jpg)
![Client1.1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/wiregaurd8.jpg)

-Interface
  - Name = xyz
  - Address = 192.168.1.2/32
  - Dns server = dns server ip address

- Peer
   - public key = Mikrotik router wiregaurd public key
   - End point = Public ip address of mikrotik.
   - Allowed ips = 0.0.0.0/0

-Setup in PC .
   - [Interface]
      - PrivateKey = your_autogenerated_private_key=
      - Address = 192.168.1.2/24
      - DNS = 192.168.100.1

   - [Peer]
      - PublicKey = your_MikroTik_public_KEY=
      - AllowedIPs = 0.0.0.0/0 [ which traffic do you want to send from tunnel, 0.0.0.0/0 means every packet is going through tunnel]
      - Endpoint = publicipaddress of mikrotik:13231

## 22.How to configure Ipsec IKEv2 VPN Server?

