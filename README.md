AWS Project: Public-Private Subnet Architecture with NAT Gateway, ALB & Auto Scaling
📌 Overview

This project demonstrates a highly available and secure AWS architecture that separates resources into public and private subnets.
The architecture is designed for scalability, security, and fault tolerance by leveraging:

VPC for network isolation

Public & Private Subnets across multiple Availability Zones

NAT Gateway for secure outbound internet access from private instances

Application Load Balancer (ALB) for distributing traffic

Auto Scaling Group (ASG) for elasticity

Security Groups for access control

S3 Gateway Endpoint for cost-efficient and secure S3 access

📊 Architecture Diagram



⚙️ Components Explained
1. Virtual Private Cloud (VPC)

Custom VPC created to host all networking components.

CIDR block defined (e.g., 10.0.0.0/16).

Provides logical isolation for resources.

2. Subnets

Public Subnets: Contain resources that need internet access (e.g., NAT Gateway, ALB).

Private Subnets: Host application servers (EC2 instances) that do not have direct internet exposure.

3. Internet Gateway (IGW)

Attached to the VPC to enable internet access for resources in the public subnet.

4. NAT Gateway

Deployed in each public subnet.

Allows instances in the private subnet to access the internet outbound only (for software updates, package downloads) without exposing them.

5. Application Load Balancer (ALB)

Placed in public subnets to handle incoming HTTP/HTTPS requests.

Distributes traffic across EC2 instances in multiple private subnets.

Improves fault tolerance and availability.

6. Auto Scaling Group (ASG)

Ensures EC2 instances in private subnets scale up or down based on demand.

Provides high availability across multiple Availability Zones.

7. EC2 Instances

Application servers running inside the private subnets.

Accessible only via ALB, not directly from the internet.

8. Security Groups

ALB SG: Allows inbound HTTP/HTTPS traffic from the internet.

EC2 SG: Allows inbound traffic only from the ALB SG.

NAT Gateway SG: Manages outbound access from private instances.

9. S3 Gateway Endpoint

Allows private subnet resources to securely access Amazon S3 without traversing the internet.

Improves performance and reduces data transfer costs.

🔄 Traffic Flow

A user accesses the application via the ALB DNS name.

The ALB routes the request to EC2 instances inside private subnets (via Auto Scaling Group).

EC2 instances process the request and may:

Access S3 directly via the S3 Gateway Endpoint.

Connect to the internet outbound via the NAT Gateway (for updates).

Responses are sent back to the ALB and then to the client.

✅ Benefits of This Architecture

High Availability: Resources deployed across multiple Availability Zones.

Scalability: Auto Scaling adjusts capacity based on load.

Security: Private subnets prevent direct internet exposure.

Cost Optimization: S3 Gateway Endpoint reduces NAT Gateway data transfer costs.

Performance: Load balancing ensures efficient traffic distribution.


📂 How to Replicate This Project

Create a VPC with CIDR block (e.g., 192.168.0.0/16).

Create public and private subnets in multiple Availability Zones.

Attach an Internet Gateway to the VPC.

Deploy NAT Gateways in public subnets.

Launch an Application Load Balancer in public subnets.

Create an Auto Scaling Group with EC2 instances in private subnets.

Configure Security Groups for ALB, EC2, and NAT Gateway.

Test the setup by accessing the ALB DNS name.

📌 Use Cases

Hosting secure web applications

Multi-tier architectures (web → app → database)

Scalable enterprise workloads

Private compute resources needing controlled internet access

🚀 Author

Abhijeet Gadge

GitHub

LinkedIn
