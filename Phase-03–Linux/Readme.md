# 🐧 Phase 3 – Linux Administration for Cloud & DevOps Engineers

> **A complete hands-on guide to Linux administration with AWS integration, production troubleshooting, real-world scenarios, and practical labs.**

---

# 📖 About This Phase

Linux is the foundation of modern Cloud Computing and DevOps.

Whether it is AWS, Azure, Google Cloud, Kubernetes, Docker, Jenkins, Terraform, Ansible, GitLab CI/CD, or Prometheus—almost every tool runs on Linux.

As a Cloud & DevOps Engineer, Linux is not simply another operating system to learn. It is the operating system you'll interact with every day while provisioning infrastructure, troubleshooting production issues, deploying applications, monitoring systems, automating tasks, and managing cloud resources.

This phase focuses on understanding Linux from an engineer's perspective instead of memorizing commands.

Every topic was practiced on an AWS EC2 instance running Amazon Linux 2023 and reinforced through quizzes, production-style troubleshooting, and a complete AWS EBS storage management lab.

The objective of this phase is not merely to execute commands but to understand:

- Why the command exists
- When it should be used
- How it helps in production
- How different Linux components work together

---

# 🎯 Learning Objectives

By completing this phase, I aimed to build a strong foundation in Linux administration that can be directly applied to Cloud and DevOps roles.

After completing this phase, I can confidently:

- Navigate the Linux filesystem
- Work efficiently with files and directories
- Understand Linux permissions and ownership
- Manage users and groups
- Monitor processes and system services
- Analyze Linux logs
- Troubleshoot common production issues
- Understand Linux networking fundamentals
- Install and manage software packages
- Compress and archive files
- Manage storage devices and filesystems
- Configure AWS EBS volumes
- Perform storage troubleshooting
- Configure persistent storage using `/etc/fstab`

---

# ☁ Why Linux Matters for Cloud & DevOps

Almost every modern cloud platform depends on Linux.

Examples include:

| Technology | Runs on Linux |
|------------|---------------|
| AWS EC2 | ✅ |
| Kubernetes | ✅ |
| Docker | ✅ |
| Jenkins | ✅ |
| GitLab Runner | ✅ |
| Terraform | ✅ |
| Prometheus | ✅ |
| Grafana | ✅ |
| NGINX | ✅ |
| Apache | ✅ |

Without Linux knowledge, troubleshooting cloud infrastructure becomes extremely difficult.

For example:

Suppose a website becomes inaccessible.

A Cloud Engineer rarely starts from the AWS Console.

Instead, they SSH into the Linux server and begin investigating:

```
Website Down

↓

SSH

↓

systemctl

↓

journalctl

↓

ss

↓

curl

↓

Logs

↓

Root Cause

↓

Resolution
```

This entire workflow depends on Linux.

---

# 🧠 Learning Philosophy

Instead of memorizing commands, this phase focused on understanding Linux from a troubleshooting perspective.

Every command was learned by answering four questions:

1. What does it do?
2. Why do we use it?
3. When should we use it?
4. How is it used in production?

This approach develops problem-solving skills rather than command memorization.

For example:

Instead of remembering:

```bash
df -h
```

The thought process becomes:

```
Application says:

"No space left on device"

↓

Check filesystem usage

↓

df -h
```

Similarly,

```
Filesystem is full

↓

Find the directory consuming space

↓

du -sh
```

Commands become solutions to problems instead of isolated syntax.

---

# 🏗 Environment Used

The entire Linux phase was completed using an AWS EC2 instance.

| Component | Details |
|-----------|----------|
| Cloud Provider | AWS |
| Compute | EC2 |
| Operating System | Amazon Linux 2023 |
| Shell | Bash |
| Filesystem | XFS |
| Package Manager | DNF |
| Architecture | x86_64 |
| SSH | OpenSSH |

Using a cloud environment instead of a local virtual machine provided practical experience with Linux in a production-like setting.

---

# 🏛 Linux Architecture

Understanding Linux architecture helps explain why commands behave the way they do.

```
+------------------------------------------------------+
|                     User Applications                |
|  Nginx | Docker | Git | Jenkins | Python | MySQL     |
+------------------------------------------------------+
|                      Shell (Bash)                    |
+------------------------------------------------------+
|                 Linux Kernel                         |
| Process Management                                  |
| Memory Management                                   |
| Device Management                                   |
| Networking                                          |
| Filesystems                                         |
+------------------------------------------------------+
|                 Hardware / AWS EC2                  |
| CPU | RAM | EBS | Network Interface | Storage        |
+------------------------------------------------------+
```

### Components

### User Applications

Applications interact with the operating system through the shell and system calls.

Examples:

- Nginx
- Docker
- Git
- Jenkins
- Python
- MySQL

---

### Shell

The shell acts as an interpreter between the user and the Linux kernel.

Example:

```bash
ls -l
```

The shell interprets this command and asks the kernel to retrieve directory information.

---

### Kernel

The kernel is the heart of Linux.

It is responsible for:

- Process scheduling
- Memory management
- Device management
- Filesystem management
- Networking
- Security

Almost every Linux command eventually interacts with the kernel.

---

### Hardware

The kernel communicates directly with the hardware.

In AWS, this includes:

- EC2 Virtual Machine
- CPU
- Memory
- Elastic Block Storage (EBS)
- Elastic Network Interface (ENI)

---

# 📂 Linux Filesystem Hierarchy

One of the first concepts every Linux administrator should understand is the Linux directory structure.

```
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── ec2-user
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

## Important Directories

### `/`

The root of the Linux filesystem.

Every file and directory originates from here.

---

### `/home`

Contains user home directories.

Example:

```
/home/ec2-user
```

This is where most day-to-day user files are stored.

---

### `/etc`

Stores configuration files.

Examples:

- `/etc/passwd`
- `/etc/hosts`
- `/etc/fstab`

As a Cloud Engineer, you'll frequently work in this directory.

---

### `/var`

Stores variable data such as:

- Logs
- Cache
- Mail
- Application data

Example:

```
/var/log
```

One of the most important directories for troubleshooting.

---

### `/tmp`

Temporary files.

Files here may be removed automatically by the operating system.

---

### `/boot`

Contains bootloader and kernel-related files required during system startup.

---

### `/dev`

Represents hardware devices as files.

Examples:

```
/dev/xvda
/dev/xvdb
```

These were used extensively during the AWS EBS storage lab.

---

### `/proc`

A virtual filesystem providing runtime information about processes and the kernel.

---

### `/mnt`

Traditionally used as a temporary mount point.

Example:

```
sudo mount /dev/xvdb /mnt
```

---

### `/opt`

Used for optional third-party software.

---

# 📘 Module Overview

This phase is divided into eight major modules.

| Module | Topics Covered |
|----------|----------------|
| Module 1 | Linux Filesystem & Navigation |
| Module 2 | Users, Groups & Permissions |
| Module 3 | Processes & Services |
| Module 4 | Logs & Troubleshooting |
| Module 5 | Linux Networking |
| Module 6 | Package Management |
| Module 7 | Archives & Compression |
| Module 8 | Disk Management & AWS EBS |

Each module combines:

- Conceptual understanding
- Hands-on practice
- Production scenarios
- Interview preparation
- AWS relevance

Together, they form the core Linux knowledge expected from a Cloud or DevOps Engineer.
