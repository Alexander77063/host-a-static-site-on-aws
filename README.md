![Alt text](/Host_a_Static_Website_on_AWS.png)

# AWS Static Website Hosting

## Project Overview
This project demonstrates the deployment of a static HTML website on AWS using a highly available, scalable, and secure infrastructure. The solution utilizes various AWS services and best practices to ensure reliability, security, and performance.

## Infrastructure Components

### Networking
- **VPC Configuration**: Multi-AZ setup with public and private subnets across two availability zones
- **Internet Gateway**: Enables communication between VPC resources and the internet
- **NAT Gateway**: Allows private subnet resources to access the internet securely
- **Security Groups**: Acts as a virtual firewall for resources

### Compute
- **EC2 Instances**: Hosts the web application in private subnets
- **Auto Scaling Group**: Automatically manages EC2 instances across multiple AZs
- **EC2 Instance Connect Endpoint**: Provides secure connection to resources in both public and private subnets

### Load Balancing
- **Application Load Balancer**: Distributes incoming traffic across multiple targets
- **Target Groups**: Manages and monitors the health of EC2 instances

### Security
- **Private Subnet Placement**: Web servers are secured in private subnets
- **AWS Certificate Manager**: Handles SSL/TLS certificates for secure communications
- **Security Groups**: Controls inbound and outbound traffic

### DNS and Domain Management
- **Route 53**: Manages domain name and DNS records
- **Custom Domain**: Registered and configured for the website

### Monitoring and Notifications
- **SNS (Simple Notification Service)**: Provides alerts for Auto Scaling Group activities

### Version Control
- **GitHub**: Stores and manages web application files

## Deployment Script
```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/Alexander77063/host-a-static-site-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-site-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-site-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Architecture Benefits

### High Availability
- Multi-AZ deployment ensures system reliability
- Auto Scaling Group maintains service availability
- Load Balancer distributes traffic across healthy instances

### Security
- Web servers in private subnets with controlled access
- SSL/TLS encryption for data in transit
- Security groups for fine-grained access control
- Secure instance access via EC2 Instance Connect Endpoint

### Scalability
- Auto Scaling Group handles varying loads
- Multi-AZ deployment supports horizontal scaling
- Load Balancer ensures even traffic distribution

### Cost Optimization
- Auto Scaling matches capacity to demand
- NAT Gateway shared across instances
- Right-sized infrastructure components

## Getting Started

1. Clone this repository
2. Configure AWS credentials
3. Deploy network infrastructure (VPC, subnets, gateways)
4. Set up security groups and EC2 Instance Connect Endpoint
5. Deploy Load Balancer and Auto Scaling Group
6. Configure SSL certificate and DNS settings
7. Deploy web application using the provided script

## Prerequisites
- AWS Account
- Registered domain name
- GitHub account
- Basic knowledge of AWS services
- AWS CLI installed and configured
