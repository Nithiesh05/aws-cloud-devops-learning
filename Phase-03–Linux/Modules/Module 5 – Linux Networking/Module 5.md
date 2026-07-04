# Module 5 – Linux Networking

---

# 📖 Introduction

Networking is the backbone of every cloud infrastructure.

Whether users are accessing a website, applications are communicating with databases, Kubernetes pods are interacting with each other, or CI/CD pipelines are deploying applications, networking is involved in every operation.

As a Cloud & DevOps Engineer, understanding Linux networking is essential because infrastructure problems are often networking problems in disguise.

Some common production incidents include:

- Unable to SSH into an EC2 instance
- Website not accessible
- API connection failures
- DNS resolution issues
- Load Balancer health check failures
- Kubernetes Pod communication failures
- Database connectivity problems

During this module, networking concepts were learned from a Linux administration perspective using an AWS EC2 instance. Instead of memorizing networking commands, the focus was placed on understanding how they help diagnose production problems.

---

# 🎯 Learning Objectives

After completing this module, I was able to:

- Understand Linux networking fundamentals
- Differentiate between public and private IP addresses
- Understand Linux network interfaces
- Verify network connectivity
- Understand hostname resolution
- Test application availability
- Troubleshoot DNS issues
- Verify listening ports
- Trace packet paths
- Apply a structured networking troubleshooting workflow

---

# Why Networking Matters

Modern applications are distributed across multiple servers.

A simple request from a user involves several networking components working together.

Example:

```
User

↓

Internet

↓

Load Balancer

↓

EC2 Instance

↓

Application

↓

Database

↓

Response
```

If communication fails at any point, the application may become unavailable.

Therefore, Linux networking knowledge is one of the most valuable troubleshooting skills for Cloud Engineers.

---

# Linux Networking Architecture

```
                     Internet
                          │
                          │
                  Internet Gateway
                          │
                          │
                      AWS VPC
                          │
        ┌─────────────────┴─────────────────┐
        │                                   │
 Public Subnet                     Private Subnet
        │                                   │
     EC2 Instance                     Database
        │
   Network Interface (ENI)
        │
      Linux Kernel
        │
      Applications
```

Networking issues may occur at any layer of this architecture.

A Cloud Engineer should investigate systematically rather than making assumptions.

---

# Public IP vs Private IP

One of the first networking concepts learned during this phase was the difference between public and private IP addresses.

## Public IP Address

A public IP address is reachable over the Internet.

Examples:

- SSH access
- Public websites
- APIs

Characteristics:

- Globally unique
- Internet accessible
- Assigned by AWS
- Can be replaced with an Elastic IP

Example:

```
54.x.x.x
```

---

## Private IP Address

Private IP addresses are used only inside a private network.

Example:

```
172.31.49.170
```

This was the private IP address assigned to the EC2 instance used throughout this phase.

Characteristics:

- Used within the VPC
- Not directly reachable from the Internet
- Used for communication between AWS resources

---

# Public vs Private IP Comparison

| Public IP | Private IP |
|------------|------------|
| Internet Accessible | Internal Communication |
| Assigned by AWS | Assigned within VPC |
| Used by external users | Used by AWS resources |
| Can change | Usually remains consistent during instance lifetime |

---

# Network Interfaces

Linux communicates with networks through network interfaces.

During this phase, the EC2 instance contained the interface:

```
enX0
```

Using Linux, we inspected:

- Interface status
- MAC address
- Private IP
- IPv6 address

Example output:

```
enX0

↓

172.31.49.170

↓

UP

↓

LOWER_UP
```

---

# Understanding Interface States

Some common interface states include:

| State | Meaning |
|---------|----------|
| UP | Interface is operational |
| DOWN | Interface disabled |
| LOWER_UP | Physical link detected |
| UNKNOWN | State cannot be determined |

Understanding interface status helps determine whether networking issues originate from Linux or AWS networking.

---

# Hostnames

Every Linux machine has a hostname.

Example:

```
ip-172-31-49-170
```

The hostname provides a human-readable identity for the machine.

Hostnames are commonly used:

- During SSH
- Within Kubernetes
- Inside monitoring systems
- During logging
- During automation

Unlike IP addresses, hostnames are easier to recognize.

---

# Connectivity Testing

One of the most important troubleshooting principles learned during this phase was:

**Always verify connectivity before investigating the application.**

A typical workflow:

```
User Cannot Access Website

↓

Verify Connectivity

↓

Verify DNS

↓

Verify Port

↓

Verify Application

↓

Investigate Logs

↓

Resolve Issue
```

This prevents unnecessary debugging of healthy applications.

---

# DNS Resolution

Applications rarely communicate using IP addresses directly.

Instead, they rely on DNS.

Example:

```
google.com

↓

DNS

↓

142.x.x.x
```

If DNS fails:

- APIs fail
- Websites become inaccessible
- Applications cannot locate databases
- Internal services cannot communicate

Therefore, DNS verification is a fundamental troubleshooting step.

---

# Packet Routing

A network packet rarely travels directly to its destination.

Instead:

```
Source

↓

Router

↓

Router

↓

Router

↓

Destination
```

Each intermediate router is known as a **hop**.

Understanding packet flow helps identify where communication fails.

---

# Port-Based Communication

Applications communicate using ports.

Examples:

| Service | Default Port |
|----------|-------------:|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |
| MySQL | 3306 |

A server may be reachable while the application itself is unavailable because the required port is not listening.

This distinction is extremely important during troubleshooting.

---

# Production Troubleshooting Workflow

One of the most valuable workflows learned during this phase is shown below.

```
User Reports

↓

Can Server Be Reached?

↓

YES

↓

DNS Working?

↓

YES

↓

Port Listening?

↓

YES

↓

Application Responding?

↓

YES

↓

Issue Resolved

↓

NO

↓

Investigate Logs
```

Notice that each step narrows the problem instead of randomly trying solutions.

---

# Production Scenario 1

## Website Not Accessible

A user reports:

> "The website is not loading."

Instead of immediately restarting NGINX, the investigation follows this sequence:

```
Verify Network

↓

Verify DNS

↓

Verify Port 80

↓

Test Locally

↓

Review Logs

↓

Restart Service (if necessary)

↓

Verify
```

This systematic approach minimizes unnecessary downtime.

---

# Production Scenario 2

## DNS Resolution Failure

Suppose an application cannot connect to an external API.

Rather than assuming the API is down:

```
Verify Network

↓

Verify DNS Resolution

↓

Confirm Correct IP Address

↓

Verify Connectivity

↓

Continue Investigation
```

This helps isolate DNS-related issues quickly.

---

# Production Scenario 3

## Packet Investigation

A destination server appears unreachable.

Instead of guessing where communication fails:

```
Trace Route

↓

Observe Each Hop

↓

Identify Failure Point

↓

Investigate Network Segment
```

Understanding packet traversal significantly improves troubleshooting accuracy.

---

# AWS Relation

Every networking concept learned during this module directly relates to AWS networking services.

| Linux Concept | AWS Service |
|---------------|-------------|
| Private IP | VPC |
| Public IP | Internet Gateway |
| DNS Resolution | Route 53 |
| Network Interface | Elastic Network Interface (ENI) |
| Ports | Security Groups |
| Routing | Route Tables |
| Connectivity | Network ACLs |

Understanding Linux networking makes AWS networking considerably easier to understand.

---

# Best Practices

✅ Verify connectivity before troubleshooting applications.

---

✅ Separate networking problems from application problems.

---

✅ Always investigate DNS before changing infrastructure.

---

✅ Verify listening ports before restarting services.

---

✅ Use a structured troubleshooting workflow.

---

# Interview Tips

### Question

What is the difference between a public IP and a private IP?

Expected Answer:

A public IP is reachable from the Internet, whereas a private IP is used for communication within a private network such as an AWS VPC.

---

### Question

Why might ping succeed while a website remains inaccessible?

Expected Answer:

The server is reachable, but the web application may not be running, the service may not be be listening on the expected port, or firewall/security rules may block the application traffic.

---

### Question

Why is DNS important?

Expected Answer:

DNS converts human-readable domain names into IP addresses, allowing applications and users to communicate without remembering numerical addresses.

---

### Question

What is a network hop?

Expected Answer:

A hop represents a router or network device through which a packet passes before reaching its destination.

---

### Question

How do you troubleshoot a website that is not accessible?

Expected Answer:

- Verify network connectivity.
- Verify DNS resolution.
- Check whether the application port is listening.
- Test the application locally.
- Review application and system logs.
- Apply corrective actions based on evidence.

---

# Key Learnings

This module fundamentally changed the way I approach networking problems.

Instead of immediately assuming an application failure, I learned to isolate the problem layer by layer.

The troubleshooting process became:

```
Network

↓

DNS

↓

Port

↓

Application

↓

Logs

↓

Resolution
```

This structured methodology reduces troubleshooting time and aligns with production support best practices.

---

# Module Summary

This module introduced Linux networking from a practical Cloud Engineering perspective.

Key skills gained include:

- Understanding Linux networking architecture
- Differentiating between public and private IP addresses
- Working with Linux network interfaces
- Understanding hostname resolution
- Verifying connectivity
- Understanding DNS
- Understanding packet routing
- Investigating port-based communication
- Applying structured networking troubleshooting workflows
- Relating Linux networking concepts to AWS infrastructure

Networking knowledge developed during this module forms the foundation for troubleshooting EC2 instances, Kubernetes clusters, Docker containers, CI/CD environments, and cloud-native applications.