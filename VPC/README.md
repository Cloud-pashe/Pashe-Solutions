Goal: Create a multi-AZ custom Virtual Private Cloud (VPC) from scratch.

Core Components:Custom CIDR block.
2 Public Subnets and 2 Private Subnets across two Availability Zones.   
Internet Gateway (IGW) attached to Public Subnets.   
NAT Gateway deployed in a Public Subnet for outbound Private Subnet connectivity.
Route Tables configured for public vs. private network paths.  


N.B: To be able to create our NAT Gateway, we needed to allocate an elastic Ip Address because the NAT Gateway needs to use it as a proxy, so when we try to access the internet from our private subnet, the NAT Gateway will mask it with this elastic IP.