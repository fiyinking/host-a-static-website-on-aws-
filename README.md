![Alt text](/Host-a-static-website-on-AWS.png)


# README for Hosting STAC Website on AWS

## Project Overview

This project details the process of hosting a STAC (SpatioTemporal Asset Catalog) HTML web application on AWS using various services to ensure high availability, security, and scalability. The infrastructure has been designed with a focus on best practices, leveraging AWS technologies.

## Architecture Diagram

![Architecture Diagram](link_to_your_architecture_diagram)  
*(Please replace with actual link to the architecture diagram)*

## Technologies Used

- **AWS Services:**
  - Virtual Private Cloud (VPC)
  - Internet Gateway
  - Security Groups
  - EC2 Instances
  - Auto Scaling Group
  - Application Load Balancer
  - NAT Gateway
  - AWS Certificate Manager
  - Simple Notification Service (SNS)
  - Route 53

- **Version Control:**
  - GitHub (for code and web files management)

## Infrastructure Setup

1. **VPC Configuration:**
   - Created a VPC with both public and private subnets across two different availability zones to enhance availability and fault tolerance.

2. **Internet Gateway:**
   - Deployed an Internet Gateway to enable communication between the VPC instances and the Internet.

3. **Security Groups:**
   - Established security groups that act as firewalls to control inbound and outbound traffic to resources.

4. **High Availability:**
   - Utilized two Availability Zones to ensure system reliability and fault tolerance.

5. **Public Subnets:**
   - Used public subnets to host infrastructure components such as the NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint:**
   - Implemented EC2 Instance Connect Endpoint to facilitate secure connections to resources in both public and private subnets.

7. **Web Servers Deployment:**
   - Positioned web servers (EC2 instances) within private subnets for enhanced security.

8. **NAT Gateway:**
   - Enabled instances in private subnets to access the Internet for updates and patches through the NAT Gateway.

9. **Website Hosting:**
   - Hosted the STAC website on EC2 instances.

10. **Load Balancer:**
    - Employed an Application Load Balancer and target group to distribute web traffic evenly to the Auto Scaling Group of EC2 instances across multiple Availability Zones.

11. **Auto Scaling Group:**
    - Utilized an Auto Scaling Group to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

12. **Version Control:**
    - Stored and versioned web files on GitHub for collaboration and tracking changes.

13. **Secure Communications:**
    - Secured application communications using AWS Certificate Manager for SSL/TLS certificates.

14. **Notifications:**
    - Configured SNS to send alerts about activities within the Auto Scaling Group.

15. **Domain Registration:**
    - Registered the domain name and set up DNS records using AWS Route 53 for smooth access to the website.

## Deployment Scripts

The scripts used to deploy the web application on the EC2 instance can be found in the GitHub repository. Follow the instructions in the repository to replicate the setup.

## Getting Started

1. Clone the repository:
   git clone <repository_url>
   

2. Follow the setup instructions in the repository to deploy the infrastructure.

3. Access the STAC website using the registered domain name.

Here below is my code
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
git clone https://github.com/fiyinking/host-a-static-website-on-aws-.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws-/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws-

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd

