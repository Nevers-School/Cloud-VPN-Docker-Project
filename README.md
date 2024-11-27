# Project 3 - Wireguard Docker Container

Create a Digital Ocean account

Create a Droplet in DigitalOcean
Use this link to DigitalOcean.com to sign up with your school email and Agent Miller’s credit card
Choose the lowest price tier - $6 per month
Create an Ubuntu droplet
Select all of the basic options
Choose password instead of ssh key - TulsaTime@1865edu
Name the project - Wireguard project
Droplet IP - 64.23.171.188

Install Wireguard 
SSH into the droplet by opening a terminal and typing ssh root@[ip]
Where you would replace [ip] with the IP of your DigitalOcean Droplet
Install the dependencies/packages needed to run docker. Commands: sudo apt install docker, sudo apt install docker-compose, sudo apt install wireguard
Set up Wireguard using Docker Compose: 
Create a directory for Wireguard: 
mkdir -p /opt/wireguard
cd /opt/wireguard
 
Create a docker-compose.yml file: 
nano docker-compose.yml
 
Add the following configuration to docker-compose.yml: 
yaml  docker-compose.yml
  GNU nano 8.1                                                        
version: '3.8'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=American/New_York
      - SERVERURL=45.55.41.235
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1


Save and exit. 

Run Wireguard: 
docker-compose up -d 
 
Check logs to get the QR code: 
docker logs wireguard 
Test Your VPN 
Mobile Device 
Open the Wireguard app and scan the QR code from the logs. 
Before connecting: 
Visit IPLeak.net and screenshot your local IP. 
After connecting: 
Turn on the Wireguard VPN and revisit IPLeak.net. 
Screenshot the VPN IP to confirm it is active. 
Laptop 
Find the configuration file: 
ls /opt/wireguard/config 
 
Copy the .conf file to your laptop. 
In our case the .conf file contained:

[Interface]
PrivateKey = iLwC8xbCzwVd5j9s7Et/72d6keAAVTlkmxcY/wX6Ako=
ListenPort = 518
.20
Address = 10.0.0.2/32
DNS = 10.0.0.1

[Peer]
PublicKey = P5GnsQQZk4X0KilGkKNg5ND/XZjV0KP7QDNuShSCcG4=
PresharedKey = 5X6AWptfcPEHqhgi3nVlEb6vx833rLQic/ofI4TMy5s=
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = 45.55.41.235:51820


Import the file into the Wireguard app or CLI. 
Follow the same steps as mobile to confirm functionality using IPLeak.net. 
 
 


Screenshots:
PC before VPN:
![unnamed](https://github.com/user-attachments/assets/1e9cfb60-40f2-45be-99a5-e7fdf9478158)
PC after VPN:
![unnamed](https://github.com/user-attachments/assets/de1377bf-bb65-44d9-ac2b-d15b17aac798)



Documentation Completed by: 
Ethan Belanger
Jalen Brown
Talha Choudhury
Levi Dunsmore
Haleigh Harris
Elise Hill
Oliver Johnson
Braden Lavarnway
Steven Lu
Nolan Miller
Kinlee Null
James Oakes
Devin Pattison
Ben Pikul
Anastasia Reed
Ahmed Al Shaqsi
Ahmad Sher
Jacob Silberfarb
Saniya Singh
Kenji Tratnik
Philip Tu
Alex Watson
Nuraiym Zhusupbekova



