# ❌ ERRORS.md

# Troubleshooting Journal

One of the primary goals of this learning journey is not only to build projects but also to develop systematic troubleshooting skills.

Every issue documented here represents a real problem encountered during the project, along with the thought process used to identify the root cause and resolve it.

---

# Error 1 – Unable to Connect to EC2 using SSH

## Problem

Unable to establish an SSH connection to the EC2 instance.

```
ssh: connect to host <Public-IP> port 22: Connection timed out
```

---

## Initial Assumption

Initially, I assumed the Security Group was blocking SSH traffic.

---

## Investigation

Verified:

* EC2 Instance State → Running ✅
* Public IPv4 Address → Available ✅
* Security Group → Port 22 Open ✅
* Route Table → Checked
* Internet Gateway → Checked

While using EC2 Instance Connect, AWS displayed:

```
Missing active route to Internet Gateway.
The Route Table contains a blackhole route.
```

---

## Root Cause

The Route Table was pointing to an old Internet Gateway that had already been deleted.

Although a new Internet Gateway was attached to the VPC, the Route Table still referenced the deleted gateway.

As a result, inbound traffic never reached the EC2 instance.

---

## Solution

* Created/attached the correct Internet Gateway.
* Updated the Route Table.
* Verified:

```
0.0.0.0/0
↓

Internet Gateway
```

SSH connectivity was restored successfully.

---

## Lesson Learned

Never assume the Security Group is the root cause.

Always verify the complete networking path:

```
Internet

↓

Internet Gateway

↓

Route Table

↓

Subnet

↓

Security Group

↓

EC2
```

---

# Error 2 – Nginx Website Not Loading

## Problem

Nginx was installed successfully, but opening the website from the browser displayed:

```
This site can't be reached
```

---

## Investigation

Verified:

* EC2 Running ✅
* Nginx Installed ✅
* Nginx Service Running ✅

Checked:

```
systemctl status nginx
```

Everything looked healthy.

---

## Root Cause

Port 80 was not allowed in the Security Group.

The EC2 instance accepted SSH connections, but HTTP requests were blocked.

---

## Solution

Added an inbound rule:

```
Type:
HTTP

Port:
80

Source:
0.0.0.0/0
```

The website loaded successfully.

---

## Lesson Learned

SSH access and HTTP access are independent.

Being able to SSH into an EC2 instance does not guarantee that a web application is reachable.

---

# Error 3 – Using HTTPS Instead of HTTP

## Problem

Opened:

```
https://<Public-IP>
```

The browser displayed an error.

---

## Root Cause

Nginx was configured only for HTTP.

HTTPS requires:

* SSL Certificate
* HTTPS Listener
* Port 443
* Nginx SSL Configuration

None of these were configured.

---

## Solution

Accessed the application using:

```
http://<Public-IP>
```

---

## Lesson Learned

HTTP and HTTPS are different protocols.

Installing Nginx alone does not automatically enable HTTPS.

---

# Error 4 – Unable to Save File in Vim

## Problem

While editing:

```
index.html
```

I was unable to save the file.

---

## Root Cause

Vim was still in Insert Mode.

Commands such as:

```
:wq
```

only work in Command Mode.

---

## Solution

1. Press ESC.
2. Type:

```
:wq
```

3. Press Enter.

---

## Lesson Learned

Understanding Vim modes is essential when working on Linux servers.

---

# Error 5 – Confusion About Route Table Associations

## Problem

After creating a new Route Table, both Public and Private Subnets were visible under the Route Table page.

Initially, I assumed both subnets were attached to the new Route Table.

---

## Root Cause

AWS was displaying:

```
Subnets without explicit associations
```

Those subnets were actually associated with the Main Route Table.

---

## Solution

Explicitly associated only the Public Subnet with the custom Public Route Table.

The Private Subnet continued using the Main Route Table.

---

## Lesson Learned

A subnet can be associated with only one Route Table.

If no explicit association exists, AWS automatically associates the subnet with the Main Route Table.

---

# Error 6 – Unable to Create a /29 Subnet

## Problem

Attempted to create:

```
10.0.1.0/29
```

AWS rejected the request.

---

## Root Cause

AWS reserves five IP addresses in every subnet.

Because of this, AWS only allows subnet sizes from /28 to /16.

---

## Solution

Created the subnet using:

```
10.0.1.0/28
```

---

## Lesson Learned

Always consider AWS reserved IP addresses while designing VPC networks.

---

# Error 7 – Public IP Not Visible in Linux

## Observation

After running:

```bash
ip addr
```

Only the Private IP was displayed.

The Public IP was missing.

---

## Understanding

Initially, I thought Linux should display both Public and Private IP addresses.

Later I learned that AWS performs Public IP translation at the Internet Gateway.

Linux primarily sees only the Private IP assigned to the network interface.

---

## Lesson Learned

The Public IP belongs to AWS networking.

The EC2 operating system mainly communicates using its Private IP.

---

# Error 8 – Wrong Troubleshooting Order

## Initial Approach

Initially, whenever something failed, I immediately checked:

* Security Groups
* Route Tables
* Internet Gateway

---

## Improved Approach

After completing this project, I adopted a structured troubleshooting methodology.

```
Is EC2 Running?

↓

Can localhost access the application?

↓

Is the service running?

↓

Is the application listening on the expected port?

↓

Check Logs

↓

Verify Security Group

↓

Verify Route Table

↓

Verify Internet Gateway

↓

Verify Public IP
```

---

## Lesson Learned

Troubleshooting should begin from the application layer and progressively move toward the network layer.

This approach significantly reduces the time required to identify the root cause.

---

# Final Reflection

The most valuable outcome of this project was not simply deploying a web server.

It was learning how to troubleshoot systematically instead of relying on trial and error.

Every issue documented here improved my understanding of AWS networking, Linux administration, and production troubleshooting.
