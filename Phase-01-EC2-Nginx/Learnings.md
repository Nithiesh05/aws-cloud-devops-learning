# 🧠 LEARNINGS.md

# Phase 1 – Key Learnings & Reflections

This document captures the most important lessons I learned while completing Phase 1 of my Cloud & DevOps learning journey.

Unlike traditional notes, this file focuses on how my understanding evolved through hands-on practice, troubleshooting, and real-world experimentation.

---

# 1. Cloud Engineering Is More Than Launching Resources

### Before

I thought learning AWS meant launching services like EC2 and following tutorials.

### After

I realized that launching an EC2 instance is only the beginning. A Cloud Engineer must also understand networking, operating systems, security, troubleshooting, and how different AWS services work together.

---

# 2. Every AWS Resource Exists to Solve a Problem

Earlier, I memorized AWS services individually.

Now I understand that every resource exists for a specific reason.

| Resource         | Problem It Solves                     |
| ---------------- | ------------------------------------- |
| EC2              | Runs applications                     |
| VPC              | Provides network isolation            |
| Subnet           | Organizes resources within a network  |
| Internet Gateway | Enables internet connectivity         |
| Route Table      | Decides where traffic should go       |
| Security Group   | Controls inbound and outbound traffic |
| Nginx            | Serves web content                    |

This way of thinking makes AWS much easier to understand.

---

# 3. Troubleshooting Is More Important Than Memorization

One of the biggest lessons from this project was learning how to troubleshoot methodically.

Initially, whenever something failed, I tried random fixes.

Now I follow a structured approach.

```text
Application

↓

Operating System

↓

Networking

↓

AWS Infrastructure
```

This reduces unnecessary guesswork and helps identify the root cause more efficiently.

---

# 4. The Importance of "Why"

Throughout this project, I focused on asking:

* Why do we need an Internet Gateway?
* Why do we need a Route Table?
* Why do we use Nginx?
* Why do we use localhost?
* Why does Linux only display the Private IP?

Understanding the reason behind each component is much more valuable than memorizing its definition.

---

# 5. Networking Is the Foundation

Initially, I viewed networking as a collection of AWS services.

Now I understand how they work together.

```text
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

↓

Nginx

↓

Web Page
```

Visualizing packet flow made networking concepts much easier to understand.

---

# 6. Public IP vs Private IP

One of the most important concepts I learned was that:

* The EC2 operating system primarily works with its Private IP.
* AWS maps the Public IP externally through the Internet Gateway.
* Running:

```bash
ip addr
```

showed only the Private IP.

This completely changed my understanding of how EC2 networking works.

---

# 7. Localhost Is a Powerful Troubleshooting Tool

Initially, I thought localhost was just another address.

Now I understand that:

```bash
curl http://localhost
```

helps determine whether the web server is functioning locally.

If localhost works but the website is inaccessible from the browser, the problem is likely in the AWS networking layer rather than the application itself.

---

# 8. Commands Should Have a Purpose

Instead of memorizing Linux commands, I learned to associate each command with a specific goal.

Examples:

| Command                | Purpose                    |
| ---------------------- | -------------------------- |
| systemctl status nginx | Check service health       |
| curl localhost         | Verify application locally |
| ss -tulnp              | Check listening ports      |
| journalctl             | View service logs          |
| ip addr                | View network interfaces    |

Understanding when to use a command is more valuable than simply knowing its syntax.

---

# 9. Documentation Is Part of Engineering

Before this project, I underestimated documentation.

Now I understand that documenting:

* Problems
* Root causes
* Solutions
* Lessons learned

helps reinforce learning and creates a valuable knowledge base for future reference.

Good documentation is also an important professional skill.

---

# 10. Mistakes Accelerate Learning

The issues I encountered taught me more than a successful deployment.

Some of the key mistakes included:

* SSH timeout caused by an incorrect Route Table.
* Missing Port 80 in the Security Group.
* Confusion between HTTP and HTTPS.
* Difficulty saving files in Vim.
* Misunderstanding Route Table associations.

Each mistake helped improve my troubleshooting skills and confidence.

---

# 11. Thinking Like a Cloud Engineer

Throughout this phase, I developed a habit of asking three questions whenever I encountered a new AWS service.

1. What problem does this service solve?
2. Why is this service required?
3. What would happen if this service were removed?

This simple framework has helped me understand AWS more deeply instead of memorizing individual services.

---

# 12. Biggest Achievement

The biggest achievement of this phase was not deploying a website.

It was changing the way I approach problems.

Instead of asking:

> "Which command should I run?"

I now ask:

> "Where is the request failing?"

This shift in thinking has made troubleshooting more structured and effective.

---

# Lessons I Will Carry Forward

As I move into the next phases of my Cloud & DevOps journey, I want to continue following these principles:

* Build first, watch tutorials second.
* Understand concepts instead of memorizing definitions.
* Document every mistake.
* Troubleshoot systematically.
* Always ask "Why?" before asking "How?"
* Learn by solving real problems.

---

# Reflection

Phase 1 gave me more than just experience with EC2 and Nginx.

It introduced me to the mindset required for Cloud Engineering.

I learned that successful engineers do not rely on memorized commands or tutorials.

They understand how systems work, follow a structured troubleshooting process, and continuously learn from every mistake they make.

This project marks the beginning of that journey, and I look forward to building on this foundation in the upcoming phases.
