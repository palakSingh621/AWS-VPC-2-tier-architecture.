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

  Step one of creating Auto-scaling group is to choose the Launch template.
