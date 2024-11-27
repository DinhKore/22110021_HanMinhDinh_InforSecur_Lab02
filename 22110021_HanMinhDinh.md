# Task 1: Firewall configuration 
**Question 1**:
- I will choose docker to do this lab
- first i will create 2 subnets (1,2) with a router forwarding traffic between them. Relevant services are also required:
- The router is initially can not route traffic between subnets
- PC0 on subnet 1 serves as a web server on subnet 1
- PC1,PC2 on subnet 2 acts as client workstations on subnet 2 
**Answer 1**:
- first i will create 2 subnets (1,2)
using
docker network create --subnet=192.168.1.0/24 subnet1
result 
dddf33bee2e388e3df3131bf51ffe8a26eb78d536c1ad5a4c89e2c96725bee21

we can see all in this
docker network ls
![image](https://github.com/user-attachments/assets/e2c32c6e-6f70-43d2-bf25-d1bcb4052c82)


using
docker network create --subnet=192.168.2.0/24 subnet2
result
223c37ee819240910f740e44bc6e098680c5d7b14f70491083a6101e1bc04aa9 
 ![image](https://github.com/user-attachments/assets/a0e1eac0-1c57-4ba6-baee-73bb1b1c4441)

after that we will creat a file name : "firewall_lab"
then we create a file docker-compose.yml
using 
version: "3.7"

services:
  pc0:
    image: nginx
    container_name: pc0
    networks:
      subnet1:
        ipv4_address: 192.168.1.10
    ports:
      - "8080:80"

  pc1:
    image: ubuntu
    container_name: pc1
    networks:
      subnet2:
        ipv4_address: 192.168.2.10
    command: bash
    stdin_open: true
    tty: true

  pc2:
    image: ubuntu
    container_name: pc2
    networks:
      subnet2:
        ipv4_address: 192.168.2.20
    command: bash
    stdin_open: true
    tty: true

  router:
    image: ubuntu
    container_name: router
    networks:
      subnet1:
        ipv4_address: 192.168.1.1
      subnet2:
        ipv4_address: 192.168.2.1
    command: bash
    stdin_open: true
    tty: true
    cap_add:
      - NET_ADMIN

networks:
  subnet1:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.1.0/24
  subnet2:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.2.0/24


we can check the file by using
Get-Content docker-compose.yml
result
![image](https://github.com/user-attachments/assets/0a3c5d07-8098-4de9-80b2-217db26c3d5d)
![image](https://github.com/user-attachments/assets/0a81333e-b2fe-4255-8210-894fbe430ad1)



**Question 2**:
- Enable packet forwarding on the router.
- Deface the webserver's home page with ssh connection on PC1
**Answer 2**:

**Question 3**:
  Config the router to block ssh to web server from PC1, leaving ssh/web access normally for all other hosts from subnet 1.   

**Answer 3**:

**Question 4**:
- PC1 now servers as a UDP server, make sure that it can reply UDP ping from other hosts on both subnets.
- Config personal firewall on PC1 to block UDP accesses from PC2 while leaving UDP access from the server intact.
**Answer 4**:


# Task 2: Encrypting large message 
Use PC0 and PC2 for this lab 
Create a text file at least 56 bytes on PC2 this file will be sent encrypted to PC0
**Question 1**:
Encrypt the file with aes-cipher in CTR and OFB modes. How do you evaluate both cipher in terms of error propagation and adjacent plaintext blocks are concerned. 
**Answer 1**:
- Demonstrate your ability to send file to PC0 to with message authentication measure.
- Verify the received file for each cipher modes
**Question 2**:
- Assume the 6th bit in the ciphered file is corrupted.
- Verify the received files for each cipher mode on PC0

**Answer 2**:

**Question 3**:
- Decrypt corrupted files on PC0.
- Comment on both ciphers in terms of error propagation and adjacent plaintext blocks criteria. 





