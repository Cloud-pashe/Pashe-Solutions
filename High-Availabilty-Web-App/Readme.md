# Goal: Deploy a resilient web application that automatically scales during traffic spikes.   

Core Components:
Multi AZ VPC Architecture
Application Load Balancer (ALB) receiving public HTTP/HTTPS traffic. 
Auto Scaling Group (ASG) launching EC2 instances across private subnets in multiple AZs.  
Custom AMI or Launch Template with user-data Bash scripts provisioning Apache/Nginx.
Target Groups for health checking EC2 fleet instances.