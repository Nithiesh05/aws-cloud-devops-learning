# 🚨 ERRORS.md

# AWS Networking - Errors & Troubleshooting

This document contains the networking issues, mistakes, and troubleshooting scenarios encountered while learning AWS Networking.

Rather than simply documenting the solution, each issue includes:

- Problem Description
- Symptoms
- Root Cause
- Investigation
- Resolution
- Lesson Learned
- Prevention

This document serves as a personal troubleshooting guide for future projects and production environments.

---

# Issue 1 - Unable to Connect Using AWS Systems Manager (SSM)

## Problem

The EC2 instance appeared healthy and running, but AWS Systems Manager Session Manager was unable to establish a connection.

---

## Symptoms

- Instance status checks passed.
- Session Manager showed:

```
Connection Failed
```

- SSM Agent status was unavailable.
- Ping status showed Offline.

---

## Investigation

The following items were verified:

- EC2 Instance State ✅
- Security Group ✅
- Route Table ✅
- Internet Connectivity ✅
- IAM Role ❌

Further investigation revealed that although an IAM role was attached, the Systems Manager service was still unable to communicate with the instance.

---

## Root Cause

The IAM Role attached to the EC2 instance was not functioning correctly.

The Systems Manager service was unable to authenticate the instance.

---

## Resolution

Detached the IAM Role from the EC2 instance.

Attached the IAM Role again.

Within a few minutes:

- Ping Status changed to Online.
- Session Manager became Available.

---

## Lesson Learned

Always verify the IAM Role before troubleshooting networking components.

Sometimes reattaching the IAM Role refreshes the instance profile association.

---

## Prevention

Whenever SSM is not working:

- Verify IAM Role
- Verify AmazonSSMManagedInstanceCore policy
- Verify SSM Agent
- Verify Internet Connectivity or VPC Endpoint
- Restart SSM Agent if necessary

---

# Issue 2 - Confusion Between Public IP and Private IP

## Problem

Expected the EC2 instance to display its Public IP address when running Linux networking commands.

---

## Symptoms

Running:

```bash
ip addr
```

Only displayed the Private IP address.

---

## Investigation

Initially assumed the Public IP should also appear inside Linux.

After understanding AWS networking architecture, it became clear that Public IP addresses are managed by AWS and translated through the Internet Gateway.

---

## Root Cause

Public IP addresses are not configured directly on the Linux network interface.

AWS performs one-to-one Network Address Translation (NAT) between the Public IP and the Private IP.

---

## Resolution

Learned the difference between:

- Public IP
- Private IP
- Internet Gateway
- NAT performed by AWS

---

## Lesson Learned

Linux only knows about its Private IP.

The Public IP exists only within AWS networking.

---

# Issue 3 - Public Subnet Misunderstanding

## Problem

Initially believed that every EC2 instance inside a Public Subnet automatically became publicly accessible.

---

## Investigation

Studied Route Tables and Public IP assignment.

Discovered that a Public Subnet only provides the possibility of internet connectivity.

An EC2 instance also requires:

- Public IP or Elastic IP
- Appropriate Security Group Rules

---

## Root Cause

Confused subnet configuration with instance configuration.

---

## Resolution

Learned that all three conditions are required:

- Public Subnet
- Public IP
- Internet Gateway Route

---

## Lesson Learned

A Public Subnet does not automatically make an EC2 instance publicly accessible.

---

# Issue 4 - Security Group vs Network ACL Confusion

## Problem

Initially assumed Security Groups and Network ACLs performed the same function.

---

## Investigation

Compared both services.

Studied request flow.

Performed multiple networking scenarios.

---

## Root Cause

Did not understand Stateful and Stateless firewalls.

---

## Resolution

Security Group

- Instance Level
- Stateful
- Allow Rules Only

Network ACL

- Subnet Level
- Stateless
- Allow and Deny Rules

---

## Lesson Learned

Security Groups should be the primary mechanism for controlling EC2 access.

Network ACLs provide an additional subnet-level security layer.

---

# Issue 5 - Route Table Association

## Problem

Initially focused only on creating Route Tables without understanding subnet association.

---

## Investigation

Studied packet flow.

Learned that AWS always checks the Route Table associated with the subnet before forwarding traffic.

---

## Root Cause

Did not understand Route Table association.

---

## Resolution

Associated the correct Route Table with the intended subnet.

Verified internet connectivity.

---

## Lesson Learned

Creating a Route Table alone is not enough.

Correct association is equally important.

---

# Issue 6 - NAT Gateway Misunderstanding

## Problem

Initially believed that NAT Gateway allows inbound internet access.

---

## Investigation

Studied request flow diagrams.

Compared Internet Gateway and NAT Gateway.

---

## Root Cause

Misunderstood NAT Gateway purpose.

---

## Resolution

Learned:

Internet Gateway

- Inbound
- Outbound

NAT Gateway

- Outbound Only

---

## Lesson Learned

Private Subnets remain private even while using NAT Gateway.

---

# Issue 7 - Troubleshooting Order

## Problem

Initially tried troubleshooting networking issues randomly.

---

## Investigation

Developed a structured troubleshooting methodology.

---

## Resolution

Adopted the following workflow.

```text
EC2 Running?

↓

Correct Subnet?

↓

Correct Route Table?

↓

Internet Gateway?

↓

Security Group?

↓

Network ACL?

↓

Public IP?

↓

IAM Role?

↓

SSM Agent?

↓

Logs
```

---

## Lesson Learned

A structured troubleshooting approach is significantly faster than randomly checking AWS resources.

---

# Common Mistakes to Avoid

- Assuming Public Subnet means Public EC2.
- Forgetting Route Table Associations.
- Ignoring IAM Roles while troubleshooting SSM.
- Confusing Security Groups with Network ACLs.
- Assuming Linux should display the Public IP.
- Troubleshooting randomly instead of following a structured process.
- Assuming Internet Gateway alone provides internet connectivity.

---

# Key Takeaways

The biggest lesson from this phase was that networking issues are rarely caused by a single component.

Successful troubleshooting requires understanding how AWS networking services work together.

A systematic investigation process is far more valuable than memorizing AWS services.

Every issue encountered during this phase reinforced the importance of verifying assumptions, understanding packet flow, and troubleshooting methodically before making changes.