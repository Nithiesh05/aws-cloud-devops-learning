# Module 1 – Linux Filesystem & Navigation

---

# 📖 Introduction

The Linux filesystem is one of the first concepts every Cloud and DevOps Engineer must master.

Unlike Windows, where files are organized using multiple drives (C:, D:, E:), Linux organizes everything under a **single hierarchical directory structure** that begins at the **root directory (`/`)**.

One of the most important philosophies in Linux is:

> **Everything is treated as a file.**

This includes:

- Regular files
- Directories
- Hard disks
- Partitions
- USB devices
- Network interfaces
- System information
- Running processes (through virtual filesystems)

Understanding the filesystem hierarchy makes Linux administration significantly easier because configuration files, logs, applications, and storage devices all follow a predictable structure.

---

# 🎯 Learning Objectives

After completing this module, I was able to:

- Navigate the Linux filesystem confidently
- Understand the Linux directory hierarchy
- Create and manage files
- Create and manage directories
- Copy, move, rename and delete files
- Search files efficiently
- View file contents
- Understand hidden files
- Work comfortably inside the Linux terminal

---

# 🏗 Linux Filesystem Hierarchy

```
                    /
                    │
 ┌──────────────────┼──────────────────┐
 │                  │                  │
etc              home               var
 │                  │                  │
Config          User Files          Logs
 │
boot
 │
Kernel
 │
dev
 │
Devices
 │
usr
 │
Applications
```

Unlike Windows:

```
C:\

D:\

E:\
```

Linux has only one root:

```
/
```

Every file and directory originates from this root directory.

---

# Important Directories

## /

The root directory.

This is the highest directory in Linux.

Everything exists under this directory.

Example:

```
/

├── etc

├── home

├── var

├── boot

├── usr

└── dev
```

---

## /home

Stores user home directories.

Example:

```
/home/ec2-user
```

This is where we performed most of our practice during this phase.

Typical contents include:

- Documents
- Downloads
- Scripts
- Practice files
- Projects

---

## /etc

Stores configuration files.

Examples:

```
/etc/passwd

/etc/hosts

/etc/fstab

/etc/nginx
```

Cloud Engineers frequently work inside this directory while configuring services.

---

## /var

Stores changing data.

Examples:

```
/var/log

/var/cache

/var/tmp
```

One of the most important directories during troubleshooting.

---

## /boot

Contains Linux kernel and bootloader files.

Without these files Linux cannot boot correctly.

---

## /dev

Contains device files.

Examples:

```
/dev/xvda

/dev/xvdb
```

These became very important during the AWS EBS lab.

---

## /tmp

Temporary storage.

Applications frequently store temporary files here.

These files may be automatically removed by Linux.

---

## /usr

Contains installed applications and libraries.

Examples:

```
/usr/bin

/usr/lib
```

---

## /opt

Typically used for optional third-party software.

---

# Navigation Commands

Navigation is the first skill every Linux administrator learns.

---

## pwd

### Purpose

Displays the current working directory.

### Syntax

```bash
pwd
```

Example

```
/home/ec2-user
```

Production Usage

Before modifying configuration files, engineers often verify their current location using `pwd`.

---

## ls

### Purpose

Lists files and directories.

### Common Options

```bash
ls
```

Basic listing

```bash
ls -l
```

Long listing

```bash
ls -a
```

Hidden files

```bash
ls -lh
```

Human-readable sizes

Example

```
Documents

Downloads

learning.txt

practice
```

Production Example

Listing log files:

```bash
ls -lh /var/log
```

---

## cd

### Purpose

Changes the current directory.

Example

```bash
cd /etc
```

Go home

```bash
cd
```

Go back

```bash
cd ..
```

Previous directory

```bash
cd -
```

Production Example

```bash
cd /var/log
```

---

# Working with Directories

---

## mkdir

Purpose

Creates directories.

Example

```bash
mkdir practice
```

Nested directories

```bash
mkdir -p project/backend/logs
```

Production Example

Creating mount points:

```bash
sudo mkdir /data
```

This was used during the EBS lab.

---

## rmdir

Removes empty directories.

Example

```bash
rmdir practice
```

---

# Working with Files

---

## touch

Creates an empty file.

Example

```bash
touch learning.txt
```

Multiple files

```bash
touch file1 file2 file3
```

---

## cp

Copies files.

Example

```bash
cp file1.txt backup.txt
```

Copy directory

```bash
cp -r project backup
```

Production Example

Backup configuration:

```bash
sudo cp /etc/nginx/nginx.conf nginx.conf.backup
```

---

## mv

Moves or renames files.

Rename

```bash
mv file1.txt learning.txt
```

Move

```bash
mv learning.txt Documents/
```

Production Example

Moving log files before cleanup.

---

## rm

Deletes files.

Example

```bash
rm learning.txt
```

Delete directory

```bash
rm -r project
```

Force delete

```bash
rm -rf project
```

⚠ Production Note

Never execute:

```bash
rm -rf /
```

or

```bash
sudo rm -rf *
```

without understanding the consequences.

---

# Viewing File Contents

---

## cat

Displays the complete file.

Example

```bash
cat learning.txt
```

Suitable for:

- Small files
- Configuration files

Not suitable for:

- Large log files

---

## less

Allows scrolling through large files.

Example

```bash
less /var/log/messages
```

Useful Shortcuts

```
/

Search

n

Next match

q

Quit
```

Production Usage

Engineers use `less` extensively while reading logs.

---

## head

Displays the beginning of a file.

Default

```bash
head file.txt
```

First 20 lines

```bash
head -20 file.txt
```

---

## tail

Displays the end of a file.

```bash
tail file.txt
```

Real-time monitoring

```bash
tail -f /var/log/messages
```

Production Usage

Monitoring application logs.

---

# Searching Files

## find

Purpose

Searches files and directories.

Example

```bash
find /home -name "*.txt"
```

Find nginx configuration

```bash
find /etc -name nginx.conf
```

Production Usage

Finding configuration files.

---

# Hidden Files

Linux files beginning with:

```
.
```

are hidden.

Example

```
.bashrc

.profile

.gitignore
```

View hidden files

```bash
ls -a
```

---

# Production Scenario

## Scenario

A developer says:

> "I cannot find the nginx configuration."

Troubleshooting

```
cd /etc

↓

find . -name nginx.conf

↓

Locate configuration

↓

Open using less

↓

Edit if required
```

---

# AWS Relation

During this module, the following AWS-related paths were explored:

```
/home/ec2-user

↓

User Home
```

```
/etc

↓

Configuration Files
```

```
/var/log

↓

System Logs
```

```
/dev/xvda

↓

Root EBS Volume
```

Understanding these directories is essential while managing EC2 instances.

---

# Best Practices

✅ Always verify your current directory using `pwd`.

✅ Prefer `cp` over `mv` before modifying important configuration files.

✅ Use `less` instead of `cat` for large files.

✅ Avoid using `rm -rf` unless absolutely necessary.

✅ Create backups before editing production configuration files.

---

# Interview Tips

### Question

What is the difference between `cp` and `mv`?

Expected Answer:

- `cp` creates a copy while preserving the original.
- `mv` moves or renames the original file.

---

### Question

Why is `less` preferred over `cat` for log files?

Expected Answer:

Because `less` allows scrolling and searching without loading the entire file into the terminal.

---

### Question

How do you search for a file in Linux?

Expected Answer:

Use:

```bash
find / -name filename
```

---

# Module Summary

This module introduced the Linux filesystem and the essential commands required for day-to-day system administration.

Key skills gained include:

- Navigating the Linux filesystem
- Managing files and directories
- Viewing file contents
- Searching files efficiently
- Understanding important Linux directories
- Developing safe file management practices

These commands form the foundation for every Cloud and DevOps activity performed on Linux systems.