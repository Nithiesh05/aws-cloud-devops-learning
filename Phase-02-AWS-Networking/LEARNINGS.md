# 📘 LEARNINGS.md

# AWS Networking - My Learnings

This document summarizes the key concepts, practical lessons, and engineering mindset I developed during Phase 2 of my Cloud & DevOps learning journey.

The goal of this document is not to repeat definitions but to capture the knowledge and understanding I gained while learning, building, troubleshooting, and solving networking-related problems in AWS.

---

# 🌐 Understanding AWS Networking

Before starting this phase, AWS networking appeared to be a collection of independent services such as VPC, Subnets, Route Tables, Internet Gateways, and Security Groups.

After completing this phase, I realized that AWS networking is an interconnected system where every component plays a specific role in controlling how traffic enters, leaves, and moves within a cloud environment.

Instead of memorizing individual services, I learned how they work together to provide secure, scalable, and reliable networking.

---

# 📌 VPC

One of the biggest realizations was understanding that a VPC is more than just a virtual network.

It provides:

- Logical isolation
- Custom IP addressing
- Network segmentation
- Traffic control
- Security boundaries

Every AWS networking component exists inside a VPC.

Without a VPC, AWS resources cannot communicate securely.

---

# 📌 CIDR Blocks

Initially, CIDR notation seemed confusing.

After multiple examples, I understood that CIDR simply defines the range of IP addresses available inside a network.

Example:

```
10.0.0.0/16
```

The CIDR block determines:

- Number of available IP addresses
- Subnet allocation
- Network scalability

Understanding CIDR made subnet creation much easier.

---

# 📌 Public and Private Subnets

One important lesson was understanding that a subnet is not public simply because of its name.

A subnet becomes Public only when:

- Its Route Table contains a route to an Internet Gateway.

Otherwise, it remains Private.

This concept is frequently asked during interviews.

---

# 📌 Route Tables

Initially, I thought creating a Route Table was enough.

Later I learned that:

Creating a Route Table has no effect until it is associated with the appropriate subnet.

AWS always checks the Route Table associated with the subnet before forwarding traffic.

Understanding Route Tables helped me visualize packet routing inside AWS.

---

# 📌 Internet Gateway

I learned that an Internet Gateway does not automatically provide internet access.

Internet connectivity depends on multiple components working together:

- Internet Gateway
- Route Table
- Public IP or Elastic IP
- Security Group

If any one of these is missing, internet connectivity fails.

---

# 📌 NAT Gateway

Initially, I assumed NAT Gateway allowed inbound internet traffic.

Later I learned:

NAT Gateway provides only outbound internet access.

This allows resources inside Private Subnets to:

- Download software
- Install updates
- Access AWS APIs

while remaining inaccessible from the internet.

---

# 📌 Security Groups

One of the biggest concepts I learned was that Security Groups are Stateful.

This means:

If inbound traffic is allowed,

AWS automatically allows the return traffic.

No separate outbound rule is required for the response.

Security Groups became much easier to understand after visualizing request and response flow.

---

# 📌 Network ACLs

Before this phase, I assumed Security Groups and Network ACLs were almost identical.

I learned that:

Security Groups

- Instance Level
- Stateful

Network ACLs

- Subnet Level
- Stateless

NACLs evaluate every request independently.

This makes them more suitable for subnet-level traffic filtering.

---

# 📌 Public IP vs Private IP

Initially, I expected Linux to display both Public and Private IP addresses.

After understanding AWS networking, I learned:

Linux only knows about its Private IP.

The Public IP exists within AWS networking and is translated by the Internet Gateway.

This clarified one of the biggest confusions I had.

---

# 📌 Elastic IP

Elastic IP is a static Public IPv4 address.

Unlike automatically assigned Public IPs, Elastic IP remains allocated until explicitly released.

This is useful for:

- Production Servers
- DNS Mapping
- Static Endpoints

---

# 📌 AWS Systems Manager (SSM)

One of the most valuable practical learnings came from troubleshooting AWS Systems Manager.

I learned that successful SSM connectivity depends on:

- Running EC2 Instance
- IAM Role
- AmazonSSMManagedInstanceCore Policy
- SSM Agent
- Internet Connectivity or VPC Endpoint

I also experienced a real issue where detaching and reattaching the IAM Role resolved the Session Manager connection problem.

This reinforced the importance of verifying IAM configuration before assuming network problems.

---

# 📌 AWS Networking Request Flow

Instead of memorizing AWS services individually, I learned to visualize request flow.

```
Browser

↓

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

EC2

↓

Application

↓

Response
```

Understanding this flow significantly improved my troubleshooting ability.

---

# 📌 Troubleshooting Mindset

Perhaps the most important lesson from this phase was developing a structured troubleshooting approach.

Instead of changing configurations randomly, I learned to investigate each networking layer systematically.

My troubleshooting sequence became:

```
EC2 Running?

↓

Subnet

↓

Route Table

↓

Internet Gateway

↓

Security Group

↓

Network ACL

↓

Public IP

↓

IAM Role

↓

SSM Agent

↓

Logs
```

Following this process reduced confusion and made troubleshooting much faster.

---

# 🚀 Production Best Practices Learned

Throughout this phase, I also learned several best practices followed in production environments.

- Use Private Subnets for backend resources.
- Expose only required services to the internet.
- Follow the Principle of Least Privilege.
- Prefer AWS Systems Manager over SSH whenever possible.
- Keep databases inside Private Subnets.
- Avoid opening unnecessary ports in Security Groups.
- Always understand packet flow before troubleshooting.

---

# 💡 How My Understanding Changed

At the beginning of this phase, I viewed AWS networking as individual services.

After completing the phase, I now understand it as a complete networking ecosystem where every component contributes to secure communication.

I also realized that successful troubleshooting depends less on memorizing AWS services and more on understanding how traffic flows through the infrastructure.

This mindset will be valuable in future phases involving Docker, Kubernetes, Terraform, CI/CD, and production deployments.

---

# 📖 Key Takeaways

- Networking is the foundation of every cloud architecture.
- Understanding packet flow is more valuable than memorizing definitions.
- Every networking issue has a logical root cause.
- Route Tables determine traffic direction.
- Internet Gateway provides internet connectivity only when routing is configured correctly.
- Security Groups and Network ACLs serve different purposes.
- AWS Systems Manager is a secure alternative to SSH.
- Troubleshooting should always follow a structured methodology.

---

# 🎯 Final Reflection

This phase transformed the way I think about cloud networking.

Rather than viewing AWS networking services as isolated components, I now understand how they interact to provide secure, reliable, and scalable communication between cloud resources and end users.

The most valuable outcome of this phase was not simply learning AWS networking concepts—it was developing the ability to analyze packet flow, identify root causes, and troubleshoot networking issues using a structured engineering approach.

This networking foundation will support every upcoming phase of my Cloud & DevOps learning journey, including Linux, Docker, Terraform, Kubernetes, CI/CD, Monitoring, and Production Infrastructure.