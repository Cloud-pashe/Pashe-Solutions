# Goal: Deploy a resilient web application that automatically scales during traffic spikes.   

Core Components:
Multi AZ VPC Architecture
Application Load Balancer (ALB) receiving public HTTP/HTTPS traffic. 
Auto Scaling Group (ASG) launching EC2 instances across private subnets in multiple AZs.  
Custom Launch Template with user-data Bash scripts provisioning Apache/Nginx.
Target Groups for health checking EC2 fleet instances.

### Note: The user data script embedded in the launch template automates the installation and configuration of the web application, ensuring that any new instance provisioned by the Auto Scaling Group is immediately ready without manual deployment overhead.

# RESULTS & EXPLANATION

The Multi-AZ VPC Architecture spans across multiple availability zones to ensure high availabilty and fault tolerance. The public subnets hosts the alb and nat gateway fot internet connectivity, while the private subnets securely isolate the EC2 web servers from direct public exposure while routing outbound traffic through the NAT Gateway.

![AWS VPC Resource Map](images/Multi%20AZ%20VPC.jpg)

The ALB security group accepts inbound HTTP (80) traffic from the internet (0.0.0.0/0), while the web server security group (web-server-sg) only accepts traffic coming from the ALB's security group.

![Security Group inbound rule](images/SG%20ALB.jpg) 
![Security Group inbound rule](images/SG%20SG%20Web%20Server.jpg)

The target group listening on the ALB does health checks on the private instances, proving that Apache is running successfully via the updated launch template. Only when the instance pass the checks,  would it be able to access our web application

![Web Target Group](images/My%20Web%20Target%20Group.jpg)
![Web App Result](images/Web%20Application%20Result.jpg)