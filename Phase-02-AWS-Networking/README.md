# 🚀 Phase 2 - AWS Networking Fundamentals & Infrastructure Design

## 📌 Project Overview

This phase of my 90-day Cloud & DevOps learning journey focused on understanding one of the most fundamental concepts in cloud computing—**AWS Networking**.

Rather than memorizing AWS networking components individually, I focused on understanding how they work together to enable secure communication between cloud resources and the internet.

The objective of this phase was to build a strong networking foundation by designing Virtual Private Clouds (VPCs), configuring subnets, route tables, Internet Gateways, Security Groups, and understanding how network traffic flows within AWS.

Throughout this phase, I intentionally spent time troubleshooting networking issues instead of immediately searching for solutions. This helped me develop a structured approach to diagnosing connectivity problems and understanding the reasoning behind each networking component.

By the end of this phase, I successfully:

- Designed custom VPC architectures.
- Understood CIDR notation and IP address allocation.
- Created Public and Private Subnets.
- Configured Route Tables.
- Attached Internet Gateways.
- Understood NAT Gateway architecture.
- Configured Security Groups and Network ACLs.
- Understood Elastic IP addresses.
- Connected to EC2 instances using AWS Systems Manager (SSM).
- Learned how AWS routes packets from the internet to EC2 instances.
- Developed a systematic troubleshooting methodology for AWS networking issues.

---

# 🎯 Objectives

The primary objectives of this phase were:

- Understand the purpose of a Virtual Private Cloud (VPC).
- Learn CIDR notation and subnetting concepts.
- Design secure AWS network architectures.
- Understand Public and Private Subnets.
- Learn how Route Tables control network traffic.
- Configure Internet Gateway connectivity.
- Understand outbound internet access using NAT Gateway.
- Learn the difference between Security Groups and Network ACLs.
- Understand Elastic IP usage.
- Learn how AWS Systems Manager (SSM) works.
- Practice AWS networking troubleshooting.
- Build networking knowledge required for production environments.

---

# 🏗️ AWS Network Architecture

```text
                               Internet
                                   │
                                   ▼
                          Internet Gateway
                                   │
                                   ▼
                    Public Route Table (0.0.0.0/0)
                                   │
          ┌────────────────────────┴────────────────────────┐
          │                                                 │
          ▼                                                 ▼
    Public Subnet                                   Private Subnet
          │                                                 │
          ▼                                                 ▼
     EC2 Web Server                              EC2 Application Server
          │                                                 │
          └─────────────── NAT Gateway ──────────────────────┘
                                   │
                                   ▼
                                Internet
```

---

# ☁️ AWS Services Used

| AWS Service | Purpose |
|-------------|----------|
| VPC | Provides an isolated virtual network for AWS resources |
| Subnets | Divide the VPC into logical network segments |
| Route Tables | Control how network traffic is routed |
| Internet Gateway | Enables internet connectivity for public resources |
| NAT Gateway | Provides outbound internet access for private resources |
| Security Groups | Instance-level firewall |
| Network ACL | Subnet-level firewall |
| Elastic IP | Static public IPv4 address |
| EC2 | Compute instance used throughout the project |
| IAM | Managed permissions for SSM access |
| AWS Systems Manager (SSM) | Secure remote access without SSH |

---

# 📋 Project Implementation

## Step 1 – Understanding AWS Networking

Before creating resources, I focused on understanding how AWS networking differs from traditional on-premise networking.

Key concepts learned:

- VPC
- CIDR Blocks
- Subnets
- Routing
- Public vs Private Networks

---

## Step 2 – Creating a Custom VPC

Created a custom VPC with an appropriate CIDR block.

Example:

```
10.0.0.0/16
```

This became the private network where all AWS resources were deployed.

---

## Step 3 – Creating Subnets

Created:

- Public Subnet
- Private Subnet

Learned:

- How subnet CIDR ranges are allocated.
- AWS reserved IP addresses.
- Minimum subnet size supported by AWS.

---

## Step 4 – Internet Connectivity

Configured:

- Internet Gateway
- Route Table
- Public Route

```
Destination

0.0.0.0/0

↓

Internet Gateway
```

This allowed resources inside the Public Subnet to communicate with the internet.

---

## Step 5 – Private Network Design

Designed a Private Subnet that had:

- No direct Internet Gateway route.
- Outbound internet access through a NAT Gateway.
- Secure communication with internal resources.

---

## Step 6 – Security Configuration

Configured:

- Security Groups
- Network ACLs

Learned:

- Stateful vs Stateless filtering.
- Inbound and Outbound rules.
- Principle of Least Privilege.

---

## Step 7 – EC2 Connectivity using AWS Systems Manager

Instead of relying only on SSH, I explored AWS Systems Manager (SSM).

Learned:

- Required IAM Role
- AmazonSSMManagedInstanceCore policy
- SSM Agent
- Session Manager

Also troubleshooted SSM connectivity issues and understood the dependency between IAM roles and the SSM Agent.

---

# 🌐 Request Flow

When a user opens a website hosted on an EC2 instance inside a Public Subnet, the request follows this path:

```text
Browser

↓

Internet

↓

Internet Gateway

↓

Route Table

↓

Public Subnet

↓

EC2 Instance

↓

Application (Nginx)

↓

Response returned to Browser
```

Understanding this request flow helped me visualize how AWS networking components work together to provide internet connectivity.

---

# 🔒 Security Flow

Traffic entering an EC2 instance passes through multiple layers.

```text
Internet

↓

Internet Gateway

↓

Route Table

↓

Subnet

↓

Network ACL

↓

Security Group

↓

EC2 Instance
```

Each component plays a different role in determining whether traffic is allowed or denied.

---

# 🔍 Troubleshooting Methodology

One of the biggest learnings from this phase was adopting a structured troubleshooting approach.

Whenever an EC2 instance was not reachable, I followed this sequence:

```text
Is the EC2 instance running?

↓

Does it have the correct subnet?

↓

Is the Route Table associated correctly?

↓

Is Internet Gateway attached?

↓

Does the Security Group allow traffic?

↓

Are Network ACLs blocking traffic?

↓

Does the EC2 have a Public IP or Elastic IP?

↓

If using SSM:

• IAM Role attached?
• SSM Agent running?
• Required permissions available?
```

This structured approach helped isolate problems quickly instead of relying on trial and error.

---

# 📚 Key Concepts Learned

During this phase, I developed a practical understanding of:

- Virtual Private Cloud (VPC)
- CIDR Blocks
- Public and Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- Elastic IP
- Public IP vs Private IP
- Stateful vs Stateless firewalls
- AWS Systems Manager (SSM)
- IAM Roles for EC2
- Packet routing inside AWS
- AWS networking best practices

---

# 🧠 Key Takeaways

Some of the most valuable lessons from this phase include:

- A subnet is considered public only when its Route Table has a route to an Internet Gateway.
- Security Groups are stateful, while Network ACLs are stateless.
- Internet Gateway alone does not provide internet connectivity; Route Tables determine where traffic is routed.
- Private Subnets should never directly expose resources to the internet.
- SSM provides secure administrative access without opening SSH (Port 22).
- Understanding packet flow is more valuable than memorizing AWS service definitions.
- Troubleshooting should always follow a structured process instead of random experimentation.

---

# 🚀 Future Improvements

This networking architecture can be enhanced by implementing:

- Multi-AZ VPC Design
- Highly Available NAT Gateway Architecture
- VPC Endpoints
- Transit Gateway
- Site-to-Site VPN
- AWS Direct Connect
- Route 53 Hosted Zones
- Application Load Balancer
- Auto Scaling Groups
- Infrastructure as Code using Terraform

---

# 📖 Documentation

Additional documents included in this phase:

- COMMANDS.md
- ERRORS.md
- INTERVIEW.md
- LEARNINGS.md
- ARCHITECTURE.md

These documents capture all commands, troubleshooting steps, interview preparation notes, architecture diagrams, and practical learnings gathered throughout this phase.

---

# 🎯 Conclusion

This phase established the networking foundation required for every Cloud Engineer. Rather than treating AWS networking services as independent components, I learned how they work together to securely connect applications, users, and cloud resources.

More importantly, I developed a systematic troubleshooting methodology that focuses on understanding packet flow, identifying root causes, and solving networking issues logically.

This project strengthened my understanding of AWS infrastructure design and prepared me for the upcoming phases involving Linux, Docker, Kubernetes, Terraform, and CI/CD, where networking remains a critical underlying component.