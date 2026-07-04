# Module 3 – Linux Processes & Services

---

# 📖 Introduction

Every application running on a Linux system executes as one or more **processes**.

Whether it is an NGINX web server, MySQL database, Jenkins server, Docker daemon, or Kubernetes component, each of them runs as a process managed by the Linux kernel.

For a Cloud and DevOps Engineer, understanding processes and services is one of the most valuable troubleshooting skills because many production incidents involve:

- Applications not starting
- Services crashing
- High CPU usage
- High memory usage
- Zombie or hung processes
- Port conflicts
- Failed deployments

During this module, I learned how Linux manages processes, how services are controlled using `systemctl`, and how to investigate application failures using production-style troubleshooting.

---

# 🎯 Learning Objectives

After completing this module, I was able to:

- Understand Linux processes
- Differentiate between a process and a service
- Monitor running processes
- Understand Process IDs (PID)
- Stop and terminate processes
- Manage Linux services
- Check service status
- Start, stop and restart services
- Investigate application failures
- Identify port conflicts

---

# 🏗 Understanding Linux Processes

A **process** is simply a program that is currently executing.

Examples include:

- NGINX
- Docker
- Jenkins
- MySQL
- SSH Server
- Python Scripts
- Java Applications

Every process is assigned a unique **Process ID (PID)** by the Linux kernel.

Example:

```
NGINX

↓

PID 1468
```

The PID uniquely identifies that running process until it exits.

---

# Process Lifecycle

```
Program

↓

Started

↓

Running Process

↓

Executing

↓

Finished

↓

Terminated
```

Every application follows this lifecycle.

---

# Process vs Service

Many beginners think these terms mean the same thing.

They do not.

| Process | Service |
|----------|----------|
| A running program | A managed application |
| Temporary | Usually long-running |
| Identified by PID | Managed by systemd |
| Can exit anytime | Starts, stops, and restarts using `systemctl` |

Example:

```
NGINX Service

↓

Managed by systemd

↓

Starts Worker Processes

↓

Each Worker has its own PID
```

---

# Understanding systemd

Modern Linux distributions use **systemd** to manage services.

Examples of services managed by systemd:

- sshd
- nginx
- docker
- crond
- firewalld

Instead of manually starting processes every time the server boots, systemd ensures services start automatically when configured.

---

# Service Lifecycle

```
Installed

↓

Enabled

↓

Started

↓

Running

↓

Stopped

↓

Restarted

↓

Disabled
```

Cloud Engineers interact with this lifecycle daily.

---

# Service Management Workflow

```
Application Not Working

↓

Check Service Status

↓

Read Logs

↓

Check Port Usage

↓

Restart Service

↓

Verify

↓

Application Restored
```

This is one of the most common production workflows.

---

# Monitoring Processes

One of the first troubleshooting steps is checking whether the process is actually running.

Common situations include:

- Application unexpectedly stopped
- High CPU utilization
- Memory consumption
- Multiple instances of the same application
- Stuck or hung processes

Instead of guessing, Linux allows engineers to inspect running processes before taking action.

---

# Process Identification

Every running process contains:

- PID
- Parent PID
- Owner
- CPU Usage
- Memory Usage
- Command

Understanding these attributes helps identify abnormal behavior during troubleshooting.

---

# Process Termination

Sometimes applications stop responding.

Examples:

- Infinite loops
- High CPU usage
- Hung deployments
- Stuck Java processes

In such cases, the process may need to be terminated safely before restarting the service.

This should always be performed carefully because killing the wrong process may interrupt production applications.

---

# Services in Production

Most production applications run as Linux services.

Examples:

```
SSH

↓

Allows remote login
```

```
NGINX

↓

Serves web traffic
```

```
Docker

↓

Runs containers
```

```
Jenkins

↓

Runs CI/CD pipelines
```

```
Cron

↓

Executes scheduled jobs
```

A Cloud Engineer spends a significant amount of time checking the health of these services.

---

# Production Scenario 1

## NGINX Website Not Accessible

A user reports:

> "The website is down."

Investigation workflow:

```
Check NGINX Service

↓

Read Logs

↓

Verify Port 80

↓

Test using curl

↓

Restart if Required

↓

Verify Website
```

This structured approach avoids unnecessary guesswork.

---

# Production Scenario 2

## Port Already in Use

During this phase, a real issue was encountered while starting NGINX.

Error:

```
Address already in use
```

Investigation:

```
Check Listening Ports

↓

Identify Process

↓

Stop Unwanted Process

↓

Restart NGINX

↓

Verify Port 80
```

This demonstrated how multiple Linux commands work together during troubleshooting.

---

# Production Scenario 3

## SSH Service Verification

To understand Linux services, the SSH daemon was investigated.

The service status and running process were verified, and process information was filtered to understand how SSH operates in the background.

This exercise demonstrated the relationship between a Linux service and the underlying processes.

---

# Production Scenario 4

## Process Search

Searching for running processes allows administrators to verify:

- Whether an application is running
- How many instances exist
- Which user owns the process

This is often one of the first steps during production troubleshooting.

---

# AWS Relation

Every EC2 instance relies on Linux services.

Examples include:

| AWS Component | Linux Service |
|---------------|---------------|
| EC2 SSH Access | sshd |
| Web Server | nginx |
| Container Runtime | docker |
| Jenkins EC2 | jenkins |
| Monitoring Agent | amazon-ssm-agent |

Understanding Linux services directly impacts cloud operations.

---

# Troubleshooting Workflow

## Application Down

```
User Reports Issue

↓

Verify Service

↓

Check Running Process

↓

Read Logs

↓

Verify Listening Port

↓

Test Connectivity

↓

Restore Service
```

This workflow was practiced repeatedly throughout this phase.

---

# Best Practices

✅ Always investigate before restarting a service.

---

✅ Prefer restarting services over rebooting the server.

---

✅ Verify whether a process is already running before starting another instance.

---

✅ Understand the difference between a service failure and an application failure.

---

✅ Investigate logs before terminating processes.

---

# Interview Tips

### Question

What is the difference between a process and a service?

Expected Answer:

A process is a running instance of a program, whereas a service is a long-running application managed by `systemd`.

---

### Question

What is a PID?

Expected Answer:

A Process ID uniquely identifies every running process in Linux.

---

### Question

Your website is down. What would you check first?

Expected Answer:

- Verify the web service is running.
- Check application logs.
- Verify the listening port.
- Test locally.
- Investigate before restarting.

---

### Question

Why shouldn't you immediately kill a process?

Expected Answer:

Because the process may belong to a production application. The root cause should be understood before terminating it.

---

### Question

Why is `systemctl` important?

Expected Answer:

It manages Linux services by allowing administrators to start, stop, restart, enable, disable, and check service status.

---

# Key Learnings

This module changed the way I approach production incidents.

Instead of assuming an application has failed, I learned to investigate systematically:

```
Service

↓

Process

↓

Logs

↓

Ports

↓

Connectivity

↓

Resolution
```

This structured troubleshooting approach is applicable not only to Linux but also to Cloud, DevOps, Kubernetes, and containerized environments.

---

# Module Summary

This module introduced Linux process and service management from a production perspective.

Key skills gained include:

- Understanding processes and services
- Interpreting process information
- Managing Linux services
- Investigating application failures
- Understanding service dependencies
- Identifying port conflicts
- Following structured troubleshooting workflows

These concepts form the foundation of production support, cloud operations, and DevOps engineering.