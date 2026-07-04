# LEARNINGS.md

# Phase 3 – Personal Learnings & Key Takeaways

---

# Introduction

Phase 3 was where I moved beyond learning Linux commands and started understanding how Linux systems work in real-world production environments.

Instead of memorizing commands, I focused on understanding:

- Why the command exists
- When to use it
- What problem it solves
- How it fits into troubleshooting
- How it relates to AWS and Cloud Engineering

One of the biggest lessons from this phase was learning to think like a System Administrator instead of simply executing commands.

---

# Module 1 – Linux Filesystem & Navigation

## What I Learned

Initially, I thought Linux was just about remembering commands like `ls`, `pwd`, and `cd`.

After practicing, I understood that the Linux filesystem is organized in a structured hierarchy and every file, configuration, and application has its own place.

I also learned the difference between:

- Absolute Path
- Relative Path

I became comfortable navigating directories and performing basic file operations using commands such as:

- pwd
- ls
- cd
- mkdir
- cp
- mv
- rm
- find
- grep

---

## Key Takeaways

- Everything in Linux is organized under the root (`/`) directory.
- Navigation commands are used continuously while administering Linux systems.
- Knowing the filesystem structure makes troubleshooting much easier.

---

# Module 2 – Users & Permissions

## What I Learned

Before this module, I knew files had permissions but did not fully understand how Linux controls access.

I learned that every file belongs to:

- Owner
- Group
- Others

Each of them can have:

- Read
- Write
- Execute

I also learned how to modify permissions using:

- chmod
- chown

and understood why using `777` is considered insecure.

---

## Key Takeaways

- Permissions are the first thing to verify when encountering "Permission denied" errors.
- Ownership is just as important as permissions.
- Following the principle of least privilege improves security.

---

# Module 3 – Processes & Services

## What I Learned

I learned the difference between a process and a service.

Initially, I thought restarting a service was always the first solution.

Now I understand that I should first investigate:

- Process status
- Service status
- Logs
- Resource usage

before restarting anything.

I also became familiar with:

- ps
- top
- systemctl
- journalctl
- dmesg

---

## Key Takeaways

- Every running application has a PID.
- Services should be investigated before being restarted.
- Logs provide valuable information during troubleshooting.

---

# Module 4 – Linux Networking

## What I Learned

This module helped me understand that networking troubleshooting should follow a structured approach.

One important realization was:

**Ping verifies connectivity, not application health.**

To verify a web application, I should use:

```bash
curl
```

I also learned the purpose of:

- ping
- curl
- wget
- ss
- nslookup
- traceroute
- nc

---

## Key Takeaways

- Connectivity and application availability are different.
- DNS issues should be isolated before troubleshooting applications.
- `ss` is useful for checking whether ports are listening.
- `traceroute` helps identify where packets are being dropped.

---

# Module 5 – Package Management

## What I Learned

I learned how Linux installs and manages software.

Initially, I thought RPM and DNF performed the same function.

Now I understand that:

- DNF automatically resolves dependencies.
- RPM installs local packages but does not resolve dependencies.

---

## Key Takeaways

- Use DNF for everyday package management.
- RPM is commonly used for vendor-provided packages.
- Repositories simplify software installation and updates.

---

# Module 6 – Archives & Compression

## What I Learned

Before this module, I thought archiving and compression were the same.

Now I understand the difference.

Archiving:

- Combines multiple files.

Compression:

- Reduces file size.

I also learned:

- tar
- gzip
- gunzip
- zip
- unzip

and understood how backups are created before production changes.

---

## Key Takeaways

- `tar` creates archives.
- `gzip` compresses files.
- `tar.gz` is commonly used for Linux backups.
- Creating backups before changes is a best practice.

---

# Module 7 – Storage Management & AWS EBS

## What I Learned

This was the most valuable module of the phase.

I learned that attaching a disk is only the beginning.

Before Linux can use a new disk, the following steps are required:

```
Attach Disk

↓

Detect Disk

↓

Create Filesystem

↓

Create Mount Point

↓

Mount Filesystem

↓

Configure /etc/fstab

↓

Verify

↓

Application Uses Storage
```

I also completed my first AWS EBS hands-on lab.

---

## Real Lesson Learned

During the lab, I encountered:

```text
Permission denied
```

Initially, I thought the mount operation had failed.

After investigating, I discovered that the mounted directory was owned by:

```
root
```

instead of:

```
ec2-user
```

Changing the ownership resolved the issue.

This taught me that successful troubleshooting requires investigation rather than guessing.

---

## Key Takeaways

- Mounting does not automatically provide write permissions.
- UUID should be used in `/etc/fstab`.
- Always verify mounts after configuration.
- Test `/etc/fstab` using `mount -a` before rebooting.
- Follow the complete storage provisioning workflow.

---

# My Troubleshooting Mindset

One of the biggest improvements during this phase was developing a structured troubleshooting approach.

Instead of trying random commands, I now follow a process:

```
Understand the Problem

↓

Collect Information

↓

Investigate

↓

Identify Root Cause

↓

Apply Fix

↓

Verify

↓

Document Learning
```

This approach helps avoid unnecessary changes and leads to faster issue resolution.

---

# Overall Learning Summary

By completing Phase 3, I strengthened my understanding of:

- Linux filesystem
- File and directory management
- Users and permissions
- Processes and services
- Linux networking
- Package management
- Archives and compression
- Storage management
- AWS EBS integration
- Linux troubleshooting

More importantly, I developed the habit of understanding **why** a command is used rather than simply memorizing its syntax.

---

# What's Next

Phase 3 has provided a solid Linux foundation for Cloud and DevOps.

The next phase will build on these skills by introducing version control and collaborative development workflows using Git and GitHub, which are essential tools for modern DevOps Engineers.

---

# Final Reflection

This phase changed the way I approach Linux.

I no longer see Linux as a collection of commands to memorize. Instead, I understand it as an operating system where every command serves a specific purpose in managing files, users, processes, networking, storage, and applications.

The most valuable lesson from this phase was learning to think systematically during troubleshooting. Rather than immediately applying fixes, I now focus on understanding the problem, identifying the root cause, and verifying the solution.

This mindset will be valuable not only for Linux administration but also for AWS, Docker, Kubernetes, Terraform, CI/CD, and every other technology I learn in the future.