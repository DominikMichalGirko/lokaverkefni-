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

6. Create (comma separated values) CSV file with the following user attributes:
7. FirstName, LastName, UserName, Department and Password. 

[klient (1).csv](https://github.com/DominikMichalGirko/lokaverkefni-/files/8149315/klient.1.csv)

8. Create a bash script that will import all user accounts into their groups
respectively. 

??

9. Each user should have his own directory under /home should use bash shell
and an encrypted password. 

![image](https://user-images.githubusercontent.com/97167360/155901197-326c5440-b4cb-4a2c-a03c-c7a2331556cd.png)

10.All users should have access to their home directory only, except the for the IT
group they should have full access to all directories. 

![image](https://user-images.githubusercontent.com/97167360/155901224-e9ae1797-93fc-4ee3-a10b-77ebc60e1b5c.png)

11.Install configure Samba then create network shared folder for each department.
All users should have full access (Read, Write and Execute Permissions) to their
shared Folder. However, IT and Management should full access to all shared
Folders. 

![image](https://user-images.githubusercontent.com/97167360/155901326-90d7c003-7409-4e8b-84bd-45c799ba6dc9.png)

![image](https://user-images.githubusercontent.com/97167360/155901333-c0939089-0fc5-4094-a2e5-e059e2923a78.png)

Samba install:

sudo apt install samba 

Configuractions :

sudo systemctl stop nmbd.service
sudo systemctl disable nmbd.service

sudo systemctl stop smbd.service

Before edit  /etc/samba/smb.conf ,Than write 
ip link

sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.orig

sudo nano /etc/samba/smb.conf

Create user 

sudo mkdir /samba/
sudo chown :sambashare /samba/

sudo mkdir /samba/my 

sudo adduser --home /samba/dominik  --no-create-home --shell /usr/sbin/nologin --ingroup sambashare dominik

sudo chmod 2770 /samba/dominik /

sudo smbpasswd -a user name
sudo smbpasswd -e user name

Then for every samba user same proces.

 /samba/everyone/:

sudo mkdir /samba/someone 
sudo adduser --home /samba/ --no-create-home --shell /usr/sbin/nologin --ingroup sambashare admin
sudo chown admin:sambashare /samba/
sudo chmod 2770 /samba/
sudo smbpasswd -a admin
sudo smbpasswd -e admin

sudo groupadd admins
sudo usermod -G admins admin

sudo nano /etc/samba/smb.conf

Test:
sudo testparm 

sudo systemctl start smbd.service

Log in:

sudo apt-get update
sudo apt-get install smbclient




12. Install and configure SSH protocol, so IT and Management users have remote
access to the server via SSH and test your configuration. 


sudo apt install openssh-server

![image](https://user-images.githubusercontent.com/97167360/156017215-a1d84bf3-748d-4fd7-a1f5-0a67e5594b2c.png)


13.Install apache2 web server with SSL certificate and configure a demo site, the
site should be accessible via the URL https://www.yourname.local

To install apache and ssl certificate

sudo apt install apache2
sudo a2enmod ssl

Copy the entire contents of the certificate from the line ----- BEGIN CERTIFICATE ----- to ----- END OF CERTIFICATE ----- and save to mydomain.crt.
Download the certificate from the mydomain.crt directory on the list of the most certified certificates, e.g .:
/ etc / ssl / certificates /
Check the Apache configuration file apache2.conf in a text editor.
Locate VirtualHost as a virtual server for the two virtual servers. The SSL certificate certificate does not require direct signing:

SSLEngine enabled - SSL in Apache
SSLCertificateFile - A certificate server that serves as an intermediate (SSL) certificate to support SSL certification
SSLCertificateKeyFile - The best way to create a private key

sudo restart apache2

To check if it works, go to the displayed https: /127.0.0.1 or https://127.0.1.1










