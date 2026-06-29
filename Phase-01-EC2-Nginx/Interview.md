# 🎤 INTERVIEW.md

# Phase 1 - EC2 & Nginx Interview Preparation

This document contains interview questions and answers based on the concepts learned during Phase 1 of my Cloud & DevOps learning journey.

The answers are written in my own words to help reinforce understanding rather than memorization.

---

# EC2

## Q1. What is Amazon EC2?

### Answer

Amazon EC2 (Elastic Compute Cloud) is a virtual server provided by AWS. It allows us to run applications in the cloud without managing physical hardware. We can choose the operating system, instance type, storage, networking, and security settings based on our application requirements.

---

## Q2. Why did you use EC2 in this project?

### Answer

I used EC2 to host a web server. The EC2 instance acted as a Linux server where I installed Nginx and hosted a static HTML webpage that could be accessed over the internet.

---

## Q3. What is an AMI?

### Answer

An Amazon Machine Image (AMI) is a template used to launch an EC2 instance. It contains the operating system and any preconfigured software required to create the server.

---

## Q4. What is an Instance Type?

### Answer

An instance type defines the CPU, memory, storage, and networking capacity of an EC2 instance. In this project, I used a t2.micro instance because it is suitable for learning and falls under the AWS Free Tier.

---

# SSH

## Q5. What is SSH?

### Answer

SSH (Secure Shell) is a secure protocol used to remotely connect to Linux servers. It encrypts the communication between the client and the server, allowing administrators to manage the server securely.

---

## Q6. What is required to SSH into an EC2 instance?

### Answer

To connect successfully, the following are required:

* EC2 instance must be running.
* Public IP or Elastic IP.
* Port 22 must be allowed in the Security Group.
* Internet Gateway and correct Route Table.
* Correct key pair.
* Correct username (for example, ec2-user for Amazon Linux).

---

## Q7. What would you check if SSH is not working?

### Answer

I follow a layered troubleshooting approach:

1. Verify the EC2 instance is running.
2. Check whether the instance has a Public IP.
3. Verify the Security Group allows SSH (Port 22).
4. Check the Route Table.
5. Verify the Internet Gateway.
6. Confirm the correct key pair and username.
7. If I have console or SSM access, verify the SSH service is running.

---

# Nginx

## Q8. What is Nginx?

### Answer

Nginx is a web server that receives HTTP requests from clients and serves web content such as HTML, CSS, JavaScript, and images. It is also commonly used as a reverse proxy and load balancer.

---

## Q9. Why did you choose Nginx?

### Answer

Nginx is lightweight, fast, and widely used in production. It is simple to configure and is a good choice for hosting static websites.

---

## Q10. Where is the default website stored?

### Answer

The default webpage is stored in:

```text
/usr/share/nginx/html
```

The main file served is:

```text
index.html
```

---

## Q11. How do you check whether Nginx is running?

### Answer

```bash
systemctl status nginx
```

---

## Q12. Difference between restart and reload?

### Answer

Restart:

* Stops the service completely.
* Starts it again.
* Existing connections may be interrupted.

Reload:

* Reloads only the configuration.
* Existing connections continue without interruption.
* Used after configuration changes.

---

## Q13. Why do we run nginx -t before reload?

### Answer

`nginx -t` checks the configuration syntax. If there is an error, we should fix it before reloading the service to avoid configuration issues.

---

# Linux

## Q14. What is localhost?

### Answer

Localhost refers to the current machine itself. When I run:

```bash
curl http://localhost
```

the request never leaves the EC2 instance. It is useful to determine whether the web server is working independently of AWS networking.

---

## Q15. Why did you use curl localhost?

### Answer

To isolate the problem.

If `curl localhost` works but the website is not accessible from the browser, the issue is likely in AWS networking (Security Groups, Route Tables, Internet Gateway, etc.).

---

## Q16. Why did you use journalctl?

### Answer

`journalctl` is used to view logs collected by systemd. I used it to check Nginx service logs during troubleshooting.

---

## Q17. What does ss -tulnp do?

### Answer

The `ss` command displays listening ports and network sockets. I used it to verify that Nginx was listening on Port 80.

---

# Networking

## Q18. Why was Port 80 opened in the Security Group?

### Answer

Port 80 allows HTTP traffic. Without opening this port, users cannot access the website from their browser.

---

## Q19. Why was Port 22 opened?

### Answer

Port 22 is required for SSH access so administrators can remotely manage the EC2 instance.

---

## Q20. What is the purpose of a Security Group?

### Answer

A Security Group acts as a virtual firewall for an EC2 instance. It controls inbound and outbound traffic based on defined rules.

---

## Q21. Explain how a request reaches your website.

### Answer

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

Response back to Browser
```

---

# Troubleshooting

## Q22. Your website is not loading. How would you troubleshoot it?

### Answer

I follow this sequence:

```text
EC2 Running?

↓

curl localhost

↓

Nginx Status

↓

Port 80 Listening

↓

Nginx Logs

↓

Security Group

↓

Route Table

↓

Internet Gateway

↓

Public IP
```

This approach helps identify whether the issue is related to the application, operating system, or AWS networking.

---

## Q23. Why did your SSH connection fail during this project?

### Answer

Initially, I suspected the Security Group. After investigating, I found that the Route Table contained a blackhole route pointing to a deleted Internet Gateway. Updating the Route Table resolved the issue.

---

# Scenario-Based Questions

## Q24. What happens if Port 80 is removed from the Security Group?

### Answer

The website becomes inaccessible from the internet, but Nginx continues running on the EC2 instance.

---

## Q25. What happens if Nginx stops?

### Answer

The EC2 instance remains running, but the website cannot serve requests until the Nginx service is started again.

---

## Q26. What happens if the Public IP is removed?

### Answer

The EC2 instance loses direct internet accessibility. Even if Nginx is running, users cannot access the website using the previous Public IP.

---

## Q27. What is the biggest lesson you learned in this project?

### Answer

The biggest lesson was learning how to troubleshoot systematically instead of guessing.

I learned to isolate the problem by starting from the application (`curl localhost`), then checking the operating system (service, ports, logs), and finally verifying the AWS networking components.

---

# Quick Revision

Before an interview, I should be able to explain:

* What is EC2?
* What is SSH?
* What is Nginx?
* Why do we use Security Groups?
* Why is Port 80 required?
* Difference between restart and reload.
* Purpose of curl localhost.
* Purpose of journalctl.
* Purpose of ss.
* Complete request flow from browser to web server.
* Structured troubleshooting methodology.

---

# Final Reflection

This phase helped me move beyond simply launching an EC2 instance.

I gained practical experience in deploying a web server, understanding the supporting AWS infrastructure, and troubleshooting real issues using a structured engineering approach.

These interview questions reinforce both the technical concepts and the practical problem-solving skills developed during the project.
