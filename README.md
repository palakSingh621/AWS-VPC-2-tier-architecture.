# AWS-VPC-2-tier-architecture.
VPC with public-private subnet in application Production

# About
![image](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/e6b4e573-d8a9-42f0-90bc-90c7497d4aa1)

To improve resiliency, the servers are deployed in two-Availabilty Zones, by using an Auto-Scaling group and an Application Load Balancer. For additional security, the serves are deployed in private subnets. The servers receive requests through the load balancer. The server can connect to the internet by using a NAT gateway. To improve resiliency, NAT gateway in both Availiablity Zones are deployed.

# Objective
* The VPC has public subnets and private subnets in two Availability Zones.
* Each public subnet contains a NAT gateway and a load balancer node.
* The server run in the private subnets, are launched and terminated by using an Auto-Scaling group, and receive Traffic from the load balancer.
* the servers can connect to the internet by using the NAT gateway.

## Step1: Creating a VPC
### VPC (Virtual Private Cloud)
A virtual private cloud (VPC) is a secure, isolated private cloud hosted within a public cloud. VPC customers can run code, store data, host websites, and do anything else they could
do in an ordinary private cloud, but the private cloud is hosted remotely by a public cloud provider.

* Create the VPC with other resources by selecting "VPC and more".
* Provide the VPC name and the IP range (i.e. 10.0.0.0/16 in this project).
* Providing two Availability-Zones for high Availability.
* Allocating 2-public and 2-private Subnets.
* Craeting 2- NAT Gateways 1 per Availibilty Zone(AZ).
* For this Project purpose, setting the VPC endpoints to None.
* Create VPC with the provided resource allocation.
![img1](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/6167655a-93b0-4880-891f-2d7f2f826356)

  ***Resource Map***
  
  ![img2](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/d091c9e9-26ea-43fb-a3af-3da462439cbd)
   <sup>Two public Subnets connected to the Internet Gateway</sup>
   
  ![img3](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/ee07fafb-8a72-4dbb-bf7e-7d971c54b787)
  <sup>1st Private Subnet connected to NAT Gateway of 1st public Subnet</sup>
  
  ![img4](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/3cbd07a6-a0b5-4196-aac2-34eff0d82e20)
  <sup>2nd Private Subnet connected to NAT Gateway of 2nd public Subnet</sup>

  ## Step2: Creating an Auto-Scaling Group
  ### Amazon EC2 Auto-Scaling
  Amazon EC2 Auto Scaling helps maintaining application availability and automatically add or remove EC2 instances using defined scaling policies. Dynamic or
  predictive scaling policies helps adding or removing EC2 instance capacity to service established or real-time demand patterns. The fleet management features of Amazon EC2 Auto
  Scaling help maintain the health and availability of your fleet.
![img5](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/9362179f-8f1c-423a-a508-f2301b230d31)

### A. Creating the Launch template
![img6](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/e099b365-d952-405b-bc7e-7e25d9f0265b)

 Setting the AMI to Ubuntu latest Version
![img7](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/80872579-f25d-43f6-bf45-40027a0826d5)

 Selecting the Key Pair.
![img8](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/f990957f-ca0d-4e97-a4bb-bb63339f1671)

Creating a Security group to allow ssh and Custom TCP for Port 8080(i.e. The hosting IP for the application) access to the VPC subnets 
![img9](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/1626b29f-0e88-48e6-a7bc-4ee1622228c0)
![img10](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/fdc70ea1-daf5-4a8a-b83f-824d9715fd34)

### B.Creating the Auto-Scaling Group
Selecting the created launch instance.
![img11](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/eeff3a6b-6f80-484d-a564-97293a949567)

Setting the VPC to define the network for Auto-scaling group.
Defining Subents,instances and Availabilty-Zones in the VPC to be used by Auto-Scaling Group.
Here, I've provided my private Sunets from my teo Availibilty Zones. 
![img12](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/89b7f8da-edd0-47cc-aa94-3e14d8056bd8)

Leaving everything else as default we create the Auto-scaling Group.
![img13](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/548fe799-5906-4acd-bde8-3f0e1578ef3b)

After Creation of Auto-Scaling Group, Two private instances are created in both the Availability-Zones.
![img14](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/fa1fb05e-12e9-4570-a322-75e6efe20285)

![img15](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/945b2865-e37a-4206-8016-df182cc95ba7)

## Step 3: Creating A Bastion Host
### Bastion Host
A bastion host is a server used to manage access to an internal or private network from an external network - sometimes called a jump box or jump server. 

Launching an Instance named Bastion-host with Ubuntu latest AMI(Amazon Machine Image).
![img16](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/488347ae-84d7-4780-9db4-ba5ed961a91c)

Providing the created VPC for the Network Connection and Enabling Auto-assigning the Public IP.
![img17](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/7ee0bf2b-81e0-4f54-9700-5697fc4c4792)

Creating a new Security Group with allowing only ssh request through the instance.
![img18](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/00fbde94-ddb4-4c2b-acac-98c19f5f48dc)

Launching the Bastion-Host instance!!
Two Public instances and a Bastion-host running...
![img19](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/177cdd42-f4be-4616-8c0d-dfe11f08fa47)

To access the Private instances through the Bastion Host we need  to copy the key pair rem file to the private instances from the local machine.


The command to copy the key Pair file from local host to the private instance:

``` scp -i <Path of the key Pair file> <Path of the key Pair file> ubuntu@<Private IP>:/home/ubuntu ```

### Problem Case1:
But running this command directly over the terminal of Windows (i.e, in my case) was not getting the job done. As it was not denying the permission to copy the keyPair file.
![img20](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/091c3c44-b5e8-4a07-a7c5-ccfe0534abe7)

To solve this problem we need to change the permissions of the Key File with the Command,

``` chmod 400 <Key_Pair>.pem```

 To configure this command in Windows:
 First enable the OpenSSL Client in Services. This will allow the Windows terminal or Command Prompt.
