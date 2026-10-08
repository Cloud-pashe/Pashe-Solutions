# Goal: Create a multi-AZ custom Virtual Private Cloud (VPC) from scratch.

Core Components:Custom CIDR block.
2 Public Subnets and 2 Private Subnets across two Availability Zones.   
Internet Gateway (IGW) attached to Public Subnets.   
NAT Gateway deployed in a Public Subnet for outbound Private Subnet connectivity.
Route Tables configured for public vs. private network paths.  


### N.B: To be able to create our NAT Gateway, we needed to allocate an elastic Ip Address because the NAT Gateway needs to use it as a proxy, so when we try to access the internet from our private subnet, the NAT Gateway will mask it with this elastic IP.

# RESULTS:
## AWS VPC Network Architecture & Egress Testing

### Architecture Overview
The custom VPC (`175.30.0.0/24`) is configured with two public subnets and two private subnets. Traffic from private subnets is routed through a NAT Gateway for outbound egress.

![AWS VPC Resource Map](images/Multi-AZ%20VPC%20result.jpg)

### Verification
Outbound connectivity from a private EC2 instance was verified using `curl` to reach external HTTPS endpoints through the NAT Gateway proxy:

![NAT Egress Curl Test](images/Instance%20result.jpg)
