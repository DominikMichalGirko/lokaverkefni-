# lokaverkefni-

1. Configure private interface of the server with a static IP address, use the first
address from the IP network: 192.168.100.0/24. 
![image](https://user-images.githubusercontent.com/97167360/155762288-df8a9c68-dbad-47af-96cf-d3d03187d42f.png)

2.After install the base system, use VI to configure hostname as server1 and domain “YourName . local”, so the FQDN of the server will be server1.yourname. local

![image](https://user-images.githubusercontent.com/97167360/155762404-799cb1c9-1ee3-4192-a0da-b66c86fb42f8.png)

![image](https://user-images.githubusercontent.com/97167360/155762426-4a4da185-a29e-449c-8948-54f5a8e6a6e7.png)
 
 3. Configure client1 hostname as client1 and FQDN as client1.yourname. local
 ![image](https://user-images.githubusercontent.com/97167360/155762610-092b4888-64e4-4190-8910-44779a4fe222.png)

4. Install and configure DHCP protocol on the server1, make sure the Client1
private interface will get an IPv4 address, Default Gateway and Domain Name
and DNS automatically from DHCP on server1. (The Default Gateway, DNS
name server is server1 IP address). 

![image](https://user-images.githubusercontent.com/97167360/155815422-a7820475-9912-426b-946e-6ac5c2f6fc14.png)

5. Install and Configure DNS on server for the internal network so hostnames are
resolved to IP addresses.

![image](https://user-images.githubusercontent.com/97167360/155818090-993133c9-6109-41d7-8825-bcafd4a8a097.png)


sudo systemctl restart bind9.service





