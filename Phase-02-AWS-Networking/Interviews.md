# 🎯 INTERVIEW.md

# AWS Networking Interview Questions & Answers

This document contains the interview questions discussed and learned during Phase 2 of my Cloud & DevOps learning journey.

The focus is not only on definitions but also on understanding how AWS networking components work together in real-world production environments.

---

# 1. What is a VPC?

A Virtual Private Cloud (VPC) is a logically isolated virtual network within AWS where cloud resources such as EC2, RDS, Lambda, and Load Balancers are deployed.

A VPC allows complete control over:

- IP Address Range
- Subnets
- Route Tables
- Internet Connectivity
- Security

---

# 2. Why do we need a VPC?

A VPC provides:

- Network Isolation
- Secure Communication
- Custom IP Addressing
- Traffic Control
- Scalability

Without a VPC, AWS resources cannot communicate securely inside a private network.

---

# 3. What is CIDR?

CIDR (Classless Inter-Domain Routing) defines the IP address range available inside a network.

Example:

```
10.0.0.0/16
```

A /16 CIDR provides 65,536 IP addresses.

---

# 4. What is a Subnet?

A subnet is a smaller network created inside a VPC.

Subnets divide the VPC into logical sections.

Examples:

- Public Subnet
- Private Subnet

---

# 5. Difference between Public and Private Subnet?

| Public Subnet | Private Subnet |
|---------------|----------------|
| Has route to Internet Gateway | No direct Internet Gateway route |
| Can communicate directly with Internet | No inbound Internet access |
| Usually hosts Web Servers | Usually hosts Databases & Internal Applications |

---

# 6. How does AWS determine whether a subnet is Public or Private?

AWS checks the Route Table associated with the subnet.

If the Route Table contains:

```
0.0.0.0/0

↓

Internet Gateway
```

the subnet is considered Public.

Otherwise it is Private.

---

# 7. What is a Route Table?

A Route Table contains rules that determine where network traffic should be forwarded.

Every subnet must be associated with a Route Table.

---

# 8. What is an Internet Gateway?

An Internet Gateway (IGW) enables communication between a VPC and the Internet.

Without an Internet Gateway, resources inside the VPC cannot communicate directly with the internet.

---

# 9. Does attaching an Internet Gateway automatically provide internet access?

No.

Internet access requires:

- Internet Gateway
- Route Table Entry
- Public IP or Elastic IP
- Appropriate Security Group Rules

All four must be configured correctly.

---

# 10. What is a NAT Gateway?

A NAT Gateway allows resources inside Private Subnets to access the internet without exposing them to inbound internet traffic.

It only supports outbound communication.

---

# 11. Difference between Internet Gateway and NAT Gateway?

| Internet Gateway | NAT Gateway |
|------------------|-------------|
| Inbound + Outbound | Outbound Only |
| Used for Public Subnets | Used for Private Subnets |
| Bidirectional Communication | One-way Internet Access |

---

# 12. What is an Elastic IP?

Elastic IP is a static Public IPv4 address provided by AWS.

Unlike normal Public IP addresses, Elastic IP remains associated with your AWS account until released.

---

# 13. Why doesn't Linux show the Public IP?

Linux only knows about its Private IP.

AWS performs Network Address Translation (NAT) between the Public IP and the Private IP using the Internet Gateway.

---

# 14. Difference between Public IP and Elastic IP?

| Public IP | Elastic IP |
|------------|------------|
| Assigned automatically | Allocated manually |
| Changes in certain scenarios | Static |
| Temporary | Persistent |

---

# 15. What is a Security Group?

A Security Group is a virtual firewall attached to an EC2 instance.

It controls:

- Inbound Traffic
- Outbound Traffic

Security Groups are Stateful.

---

# 16. What does Stateful mean?

If inbound traffic is allowed, the return traffic is automatically allowed.

No additional outbound rule is required.

---

# 17. What is a Network ACL?

Network ACL (NACL) is a subnet-level firewall.

It filters traffic entering and leaving an entire subnet.

---

# 18. Difference between Security Group and Network ACL?

| Security Group | Network ACL |
|----------------|-------------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Allow Rules Only | Allow and Deny Rules |

---

# 19. Which is evaluated first?

Traffic reaches the subnet first.

Evaluation order:

```
Network ACL

↓

Security Group

↓

EC2 Instance
```

---

# 20. What is AWS Systems Manager (SSM)?

AWS Systems Manager allows secure management of EC2 instances without opening SSH (Port 22).

---

# 21. What are the requirements for Session Manager?

- Running EC2 Instance
- IAM Role attached
- AmazonSSMManagedInstanceCore Policy
- Running SSM Agent
- Internet Connectivity or VPC Endpoint

---

# 22. How would you troubleshoot if SSM is not connecting?

My troubleshooting approach:

```
EC2 Running?

↓

IAM Role Attached?

↓

Correct IAM Policy?

↓

SSM Agent Running?

↓

Internet Connectivity?

↓

VPC Endpoint (if Private Subnet)?

↓

Restart Agent

↓

Review Logs
```

---

# 23. How do you identify whether a subnet is Public or Private during an interview?

I check the Route Table associated with the subnet.

If it contains:

```
0.0.0.0/0

↓

Internet Gateway
```

then it is Public.

Otherwise it is Private.

---

# 24. Explain the request flow when a user opens a website hosted on EC2.

```
Browser

↓

DNS

↓

Public IP

↓

Internet Gateway

↓

Route Table

↓

Subnet

↓

Security Group

↓

EC2 Instance

↓

Nginx

↓

Application

↓

Response
```

---

# 25. Explain the packet flow inside AWS.

```
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

---

# 26. Can an EC2 instance inside a Public Subnet remain private?

Yes.

If it does not have a Public IP (or Elastic IP), it cannot be accessed directly from the internet, even though it resides in a Public Subnet.

---

# 27. Why do we use Private Subnets?

To protect backend resources such as:

- Databases
- Internal APIs
- Application Servers

Private Subnets reduce the attack surface by preventing direct internet access.

---

# 28. What is the Principle of Least Privilege?

Grant users, applications, and services only the permissions required to perform their tasks—nothing more.

This minimizes security risks and follows AWS security best practices.

---

# 29. Real Interview Scenario

### Question

Your website is not accessible.

How will you troubleshoot?

### Answer

1. Verify EC2 Instance State.
2. Verify Public IP.
3. Verify Security Group Rules.
4. Verify Route Table.
5. Verify Internet Gateway.
6. Verify Network ACL.
7. Verify Web Server (Nginx).
8. Verify Application Logs.

---

# 30. Real Interview Scenario

### Question

SSM is not connecting.

How will you troubleshoot?

### Answer

1. Verify EC2 Instance is Running.
2. Verify IAM Role.
3. Verify AmazonSSMManagedInstanceCore Policy.
4. Verify SSM Agent Status.
5. Verify Internet Connectivity or VPC Endpoint.
6. Restart SSM Agent if necessary.
7. Review SSM Logs.

---

# Interview Tips

- Don't memorize definitions. Understand packet flow.
- Always explain "why" along with "what".
- Mention real troubleshooting experiences whenever possible.
- Draw request flow diagrams if asked.
- Use production examples to support your answers.
- Follow a structured troubleshooting approach instead of guessing.

---

# Final Takeaway

The biggest lesson from this phase is that AWS networking is not about individual services. It is about understanding how all networking components work together to securely deliver traffic between users and cloud resources.

During interviews, demonstrating your understanding of request flow, troubleshooting methodology, and production scenarios creates a much stronger impression than simply recalling AWS service definitions.