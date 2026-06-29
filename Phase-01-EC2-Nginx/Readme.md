# 🚀 Phase 1 - Deploying a Static Website on AWS EC2 using Nginx

## 📌 Project Overview

This project marks the beginning of my 90-day Cloud & DevOps learning journey. The objective of this phase was not just to launch an EC2 instance, but to understand the complete lifecycle of hosting a website on AWS while learning how the underlying networking components work together.

Instead of following a tutorial step by step, I focused on understanding the purpose of each AWS resource, troubleshooting real issues, documenting every mistake, and learning how to think like a Cloud Engineer.

By the end of this project, I successfully:

- Created and configured an EC2 instance.
- Connected to the server using SSH.
- Installed and configured Nginx.
- Hosted a custom HTML webpage.
- Understood the relationship between VPC, Subnets, Route Tables, Internet Gateway, Security Groups, and EC2.
- Learned a structured troubleshooting methodology for web server connectivity issues.

---

# 🎯 Objectives

The primary objectives of this project were:

- Learn how to launch an EC2 instance.
- Understand SSH connectivity.
- Install and manage Nginx.
- Host a static HTML webpage.
- Learn basic Linux administration.
- Understand AWS networking fundamentals.
- Practice troubleshooting instead of relying on tutorials.
- Build documentation using real-world engineering practices.

---

# 🏗️ Architecture

```text
                        Internet
                            │
                            ▼
                   Internet Gateway
                            │
                            ▼
                 Public Route Table
           (0.0.0.0/0 → Internet Gateway)
                            │
                            ▼
                    Public Subnet
                            │
                            ▼
                   EC2 (Amazon Linux)
                            │
                            ▼
                         Nginx
                            │
                            ▼
                     Custom HTML Page
```

---

# ☁️ AWS Services Used

| AWS Service | Purpose |
|-------------|----------|
| EC2 | Hosted the web server |
| VPC | Provided network isolation |
| Public Subnet | Hosted the EC2 instance |
| Internet Gateway | Enabled internet connectivity |
| Route Table | Routed internet traffic |
| Security Group | Allowed SSH and HTTP traffic |

---

# 💻 Linux Tools & Commands Used

| Command | Purpose |
|----------|----------|
| ssh | Connect to EC2 |
| pwd | Print working directory |
| ls -l | List files |
| vim | Edit HTML files |
| systemctl | Manage Nginx service |
| ss -tulnp | Verify listening ports |
| curl localhost | Test the web server locally |
| journalctl | View Nginx service logs |
| stat | Display file information |
| tail | View access and error logs |

---

# 📋 Project Implementation

## Step 1 – Launch EC2 Instance

- Created an Amazon Linux EC2 instance.
- Enabled Public IPv4 Address.
- Created a Security Group.
- Allowed:
  - SSH (22)
  - HTTP (80)

---

## Step 2 – Connect to EC2

Connected to the instance using PuTTY and verified connectivity.

Commands used:

```bash
whoami
hostname
pwd
```

---

## Step 3 – Install Nginx

Installed Nginx using the package manager.

```bash
sudo yum install nginx -y
```

Verified installation.

```bash
nginx -v
```

---

## Step 4 – Start and Enable Nginx

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

Verified service status.

```bash
systemctl status nginx
```

---

## Step 5 – Verify Website

Opened:

```
http://<Public-IP>
```

Verified that the default Nginx webpage loaded successfully.

---

## Step 6 – Replace Default Webpage

Located:

```
/usr/share/nginx/html/index.html
```

Edited the file using Vim.

Created a custom HTML page.

Verified that the browser displayed the new webpage.

---

# 🌐 Request Flow

When a user opens:

```
http://<Public-IP>
```

The request follows this path:

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

Nginx

↓

index.html

↓

Response returned to Browser
```

Understanding this request flow helped me visualize how AWS networking components work together.

---

# 🔍 Troubleshooting Approach

One of the biggest learnings from this project was developing a structured troubleshooting methodology instead of randomly trying commands.

Whenever the website was not accessible, I followed this order:

```text
Is EC2 Running?

↓

Can I access localhost?

↓

Is Nginx Running?

↓

Is Port 80 Listening?

↓

Check Nginx Logs

↓

Verify Security Group

↓

Verify Route Table

↓

Verify Internet Gateway

↓

Verify Public IP
```

This approach helped isolate whether the problem was related to the application, operating system, or AWS networking.

---

# 📚 Key Concepts Learned

During this project, I gained a practical understanding of:

- EC2 lifecycle
- SSH connectivity
- Security Groups
- Public IP vs Private IP
- Internet Gateway
- Route Tables
- Public Subnets
- Nginx Web Server
- Linux services
- Systemd
- Basic Linux troubleshooting
- HTTP request flow

---

# 🧠 Key Takeaways

Some of the most important lessons I learned during this project include:

- Internet Gateway alone does not provide internet connectivity.
- Route Tables determine where traffic is routed.
- Nginx listens on `0.0.0.0:80`, not on the Public IP.
- Linux primarily sees the Private IP; AWS maps the Public IP externally.
- `curl localhost` is one of the best commands to determine whether an issue is related to the application or networking.
- Troubleshooting should begin from the application layer and move outward toward the network.
- Understanding the "why" behind each AWS resource is more valuable than memorizing definitions.

---

# 🚀 Future Improvements

This project can be enhanced by implementing:

- HTTPS using SSL/TLS
- Domain Name with Route 53
- Elastic IP
- Load Balancer
- Auto Scaling Group
- Dockerizing the application
- CI/CD using GitHub Actions
- Infrastructure as Code using Terraform

---

# 📖 Documentation

Additional documents included in this project:

- ERRORS.md
- COMMANDS.md
- INTERVIEW.md
- LEARNINGS.md

These documents capture troubleshooting steps, commonly used commands, interview preparation notes, and key learnings from the project.

---

# 🎯 Conclusion

This project served as the foundation for my Cloud & DevOps learning journey. More than simply deploying a web server, it helped me understand how AWS networking, Linux administration, and web servers interact in a real-world environment.

The focus throughout this project was not only on completing the implementation but also on understanding the reasoning behind every configuration, troubleshooting issues systematically, and documenting the learning process.

This repository represents the first milestone in building practical Cloud & DevOps skills through hands-on projects.