# ERRORS.md

# Phase 3 – Linux Troubleshooting & Root Cause Analysis

---

# Introduction

This document contains the common Linux errors encountered during Phase 3 while learning Linux administration on AWS EC2.

Instead of simply listing error messages, each issue includes:

- Symptoms
- Root Cause
- Investigation
- Resolution
- Prevention

This document reflects real troubleshooting scenarios that a Linux Administrator, Cloud Engineer, or DevOps Engineer may encounter in production.

---

# Error 1 – Permission Denied

## Error

```text
Permission denied
```

---

## Symptoms

- Unable to create files
- Unable to modify files
- Unable to execute scripts
- Unable to write to mounted storage

---

## Possible Root Causes

- Incorrect file permissions
- Wrong file ownership
- Missing execute permission
- Mounted directory owned by another user

---

## Investigation

Check file permissions

```bash
ls -l file.txt
```

Check ownership

```bash
ls -ld /data
```

Check current user

```bash
whoami
```

Display detailed information

```bash
stat file.txt
```

---

## Real Scenario

During the AWS EBS lab, a new filesystem was mounted at:

```text
/data
```

Creating a file resulted in:

```text
Permission denied
```

Investigation showed:

```text
Owner

↓

root
```

Current user:

```text
ec2-user
```

The mounted directory belonged to the root user, preventing write access.

---

## Resolution

Change ownership

```bash
sudo chown -R ec2-user:ec2-user /data
```

Verify

```bash
ls -ld /data
```

---

## Prevention

- Verify ownership after mounting a new filesystem.
- Avoid using root-owned directories for application data unless required.

---

# Error 2 – Command Not Found

## Error

```text
command not found
```

Example:

```bash
findmet
```

Output

```text
-bash: findmet: command not found
```

---

## Possible Root Causes

- Typographical error
- Command not installed
- PATH environment issue

---

## Investigation

Verify spelling

Check command location

```bash
which findmnt
```

---

## Resolution

Correct the command

```bash
findmnt
```

---

## Prevention

- Verify command spelling.
- Use tab completion where possible.

---

# Error 3 – Port Already in Use

## Error

```text
bind() failed (98: Address already in use)
```

---

## Symptoms

Application fails to start.

NGINX does not start.

---

## Investigation

Check listening ports

```bash
ss -tulnp
```

Filter specific port

```bash
ss -tulnp | grep 80
```

Identify process

```bash
ps -ef | grep nginx
```

---

## Root Cause

Another application was already listening on the required port.

---

## Resolution

Stop the conflicting application.

Restart the required service.

---

## Prevention

Always verify port usage before starting a service.

---

# Error 4 – Device or Resource Busy

## Error

```text
umount: target is busy
```

---

## Symptoms

Filesystem cannot be unmounted.

---

## Root Cause

A process is still using the mounted filesystem.

Examples:

- Current terminal inside mount directory
- Running application
- Open file

---

## Investigation

Determine current directory

```bash
pwd
```

Check open files

```bash
lsof +D /data
```

---

## Resolution

Exit the directory

Stop applications

Retry

```bash
sudo umount /data
```

---

## Prevention

Ensure no applications are using the filesystem before unmounting.

---

# Error 5 – Filesystem Not Mounted

## Symptoms

Files expected inside a mounted directory are missing.

---

## Investigation

Verify mount

```bash
findmnt
```

or

```bash
mount
```

Check fstab

```bash
cat /etc/fstab
```

---

## Root Cause

Filesystem not mounted.

or

Temporary mount disappeared after reboot.

---

## Resolution

Mount again

```bash
sudo mount /dev/xvdb /data
```

Configure persistence

```text
/etc/fstab
```

Test

```bash
sudo mount -a
```

---

## Prevention

Always configure persistent mounts using UUID.

---

# Error 6 – New EBS Volume Not Visible

## Symptoms

Newly attached EBS does not appear.

---

## Investigation

Display block devices

```bash
lsblk
```

Check kernel messages

```bash
dmesg
```

---

## Root Cause

- Volume not attached
- Wrong Availability Zone
- Operating system has not detected device

---

## Resolution

Verify attachment in AWS Console.

Recheck

```bash
lsblk
```

---

## Prevention

Always verify the volume is attached to the correct EC2 instance in the same Availability Zone.

---

# Error 7 – No Filesystem Found

## Symptoms

Mount command fails.

---

## Root Cause

Filesystem not created.

---

## Investigation

Display filesystem

```bash
lsblk -f
```

or

```bash
blkid
```

If no filesystem exists,

Linux cannot mount it.

---

## Resolution

Create filesystem

```bash
sudo mkfs.xfs /dev/xvdb
```

Mount again.

---

## Prevention

Always create a filesystem before mounting a new disk.

---

# Error 8 – Wrong UUID in /etc/fstab

## Symptoms

System fails to mount storage after reboot.

---

## Investigation

Check UUID

```bash
blkid
```

Compare with

```bash
cat /etc/fstab
```

---

## Root Cause

Incorrect UUID configured.

---

## Resolution

Update the correct UUID.

Test

```bash
sudo mount -a
```

---

## Prevention

Never type UUID manually.

Always copy using

```bash
blkid
```

---

# Error 9 – No Space Left on Device

## Error

```text
No space left on device
```

---

## Investigation

Filesystem usage

```bash
df -h
```

Directory usage

```bash
du -sh /*
```

---

## Root Cause

Filesystem is full.

Large log files.

Application data.

---

## Resolution

Identify large directories.

Archive logs.

Delete unnecessary files.

Extend storage if required.

---

## Prevention

Monitor storage regularly.

---

# Error 10 – DNS Resolution Failed

## Symptoms

Website unreachable.

Ping by IP works.

Ping by hostname fails.

---

## Investigation

DNS lookup

```bash
nslookup google.com
```

Test connectivity

```bash
ping 8.8.8.8
```

---

## Root Cause

DNS server unavailable.

DNS configuration issue.

---

## Resolution

Verify DNS server.

Check network connectivity.

---

## Prevention

Always separate DNS issues from connectivity issues.

---

# Error 11 – Application Running but Website Not Accessible

## Symptoms

NGINX running.

Website inaccessible.

---

## Investigation

Verify service

```bash
systemctl status nginx
```

Verify port

```bash
ss -tulnp | grep 80
```

Test locally

```bash
curl localhost
```

---

## Possible Root Causes

- Firewall
- Security Group
- Wrong port
- Reverse proxy issue

---

## Resolution

Verify networking.

Verify Security Group.

Verify application configuration.

---

# Error 12 – Package Installation Failed

## Symptoms

Package installation unsuccessful.

---

## Investigation

Verify repositories

```bash
dnf repolist
```

Search package

```bash
dnf search nginx
```

Display package information

```bash
dnf info nginx
```

---

## Possible Root Causes

- Repository unavailable
- Network issue
- Incorrect package name

---

## Resolution

Update metadata

```bash
sudo dnf clean all
```

Retry installation.

---

# Error 13 – RPM Dependency Error

## Symptoms

RPM installation fails.

---

## Root Cause

Required dependencies missing.

---

## Investigation

Attempt installation

```bash
rpm -ivh package.rpm
```

---

## Resolution

Prefer

```bash
sudo dnf install package.rpm
```

DNF automatically resolves dependencies.

---

# General Linux Troubleshooting Workflow

```
Problem Reported

↓

Read Error Message

↓

Understand Symptoms

↓

Check Logs

↓

Verify Permissions

↓

Verify Services

↓

Verify Processes

↓

Verify Networking

↓

Verify Storage

↓

Identify Root Cause

↓

Apply Fix

↓

Verify Resolution

↓

Document Learning
```

---

# Key Takeaways

- Never assume the cause of an issue.
- Always investigate before applying a fix.
- Read the complete error message.
- Verify permissions, ownership, networking, storage, and services systematically.
- Test the solution before considering the issue resolved.
- Document every issue to improve future troubleshooting efficiency.

---

# Final Note

The most valuable lesson from this phase was understanding that effective troubleshooting is not about memorizing commands—it is about following a structured investigation process.

A disciplined workflow such as:

```
Observe

↓

Investigate

↓

Identify Root Cause

↓

Fix

↓

Verify

↓

Document
```

is far more effective than trying random solutions. This mindset is essential for Linux Administrators, Cloud Engineers, DevOps Engineers, and Site Reliability Engineers working in production environments.