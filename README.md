# AWS-VPC-2-tier-architecture.
VPC with public/private subnet in application Production

# About
![image](https://github.com/palakSingh621/AWS-VPC-2-tier-architecture./assets/107800373/e6b4e573-d8a9-42f0-90bc-90c7497d4aa1)
To improve resiliency, the servers are deployed in two-Availabilty Zones, by using an Auto-Scaling group and an Application Load Balancer. For additional security, the serves are deployed in private subnets. The servers receive requests through the load balancer. The server can connect to the internet by using a NAT gateway. To improve resiliency, NAT gateway in both Availiablity Zones are deployed.

# Objective
* The VPC has public subnets and private subnets in two Availability Zones.
* Each public subnet contains a NAT gateway and a load balancer node.
* The server run in the private subnets, are launched and terminated by using an Auto-Scaling group, and receive Traffic from the load balancer.
* the servers can connect to the internet by using the NAT gateway.

