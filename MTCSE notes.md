# MTCSE
**1. How to we upgrade router OS and firmware verion**
- System > Check for updates > Download and install.
![Router OS Upgrade](https://github.com/Rajeev-Tamang/MTCSE/blob/main/RouterOS%20Upgrade.jpg)

**2. How to upgrade router board firmware?**
- System > RouterBoard > Upgrade > Reboot for change.
![Router Board Firmware Upgrade](https://github.com/Rajeev-Tamang/MTCSE/blob/main/router%20Board%20firmware%20upgradejpg.jpg)

**3. How do we control access to mikrotik router?**

**Note**: ***Removing the defualt admin user after creating new user with full access or setting strong password for admin user is highly recomended.***
 
- Ip address of mikrotik router is: 172.16.210.210/24
- Allowed address for user rajeev is : 172.16.210.239/24
![Allowed user and ip address](https://github.com/Rajeev-Tamang/MTCSE/blob/main/allowed%20user%20and%20ip%20address.jpg)

![IP address before](https://github.com/Rajeev-Tamang/MTCSE/blob/main/ip%20address%20before.jpg)

![Login Failed](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Login%20Failed.jpg)
- Since ip address is 172.16.210.233/24 , it is not accesible. Lets Change the ip address and try again.
![Allowed Ip address](https://github.com/Rajeev-Tamang/MTCSE/blob/main/Login%20allowed.jpg)
-Now User: rajeev with ip address 172.16.210.239 is allowed to access.

**4. How do we disable and Change service port?**
- IP > Services > Select > Enable ✅	/ Disable ❌
![IP Service port](https://github.com/Rajeev-Tamang/MTCSE/blob/main/service%20port%20enable%20disable%20change.jpg)

***Note: If you do not use certain services , its recommended to disable it***
  ***Changing service port is also highly recommeded , default winbox port is 8291**

***5. How do we disable MAC access.?*** 
- Tools > Mac server > Mac telnet / Mac winbox / Mac Ping.
![Mac ping](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20ping%20%20server.jpg)

![Mac Telnet](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20telnet%20server.jpg)

![Mac winbox](https://github.com/Rajeev-Tamang/MTCSE/blob/main/mac%20winbox%20server.jpg)

***Note: In production network is not a good pratice to enable mac access, mac ping mac telnet.***

**6. How do we diasble neighbor discovery?**
- IP > Neighbor > Discovery Setting >  Interface > None > Apply.
![Neigbor discovery Disable](https://github.com/Rajeev-Tamang/MTCSE/blob/main/neighbor%20disable.jpg)

***Note: We see neighbor in winbox table, it is highly recommended to disable the Neighbor discovery***


**7. How do we disable ping request from firewall?**
- IP > Firewall > ADD > Chain = Input > source address=0.0.0.0/0 > Protocol= ICMP > Action = drop > Apply > Ok

![Firewall rule 1](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%201.jpg)

![Firewall rule 2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%202.jpg)

![Firewall rule 3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/firewall%20rule%203.jpg)


**8. How to use Forward Chain**
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


**9. How do we use Output Chain**

- Output chain processess packets originatin from the router itself.

- Suppose we want to Block the icmp packet form our mikrotik to cloudflare dns 1.1.1.1 
  then, 
- IP > Firewall > Filter Rules > ADD > Chain = Output > Protocol = ICMP > out.interface 
  = Ether1 > Action = drop > Apply > OK.

![output chain](https://github.com/Rajeev-Tamang/MTCSE/blob/main/outputchain%201.jpg)

![Output chain2](https://github.com/Rajeev-Tamang/MTCSE/blob/main/output%20chain%202.jpg)

![Output Chain3](https://github.com/Rajeev-Tamang/MTCSE/blob/main/output%20chain3.jpg)


**10. Soure NAT**

- IP > Firewall > NAT > ADD > Chain = Srcnat > Action = masquerade > Apply > OK.


**11. How can i redirect traffic from one port to another?**

- Destination NAT or dstant. It is most commonly used to make hosts on a private 
  netwrok to be accessible from the internet.

- 
