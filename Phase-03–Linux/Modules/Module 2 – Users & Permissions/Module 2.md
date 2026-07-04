# Module 2 – Linux Users, Groups & File Permissions

---

# 📖 Introduction

Linux is a multi-user operating system designed to allow multiple users and applications to work securely on the same machine.

Every file, process, service, and directory in Linux belongs to a user and a group. The Linux permission model ensures that users can only access resources they are authorized to use.

For Cloud and DevOps Engineers, understanding Linux permissions is one of the most important skills because many production issues are directly related to incorrect ownership or file permissions.

During this module, we explored how Linux manages users, groups, ownership, permissions, and administrative privileges.

---

# 🎯 Learning Objectives

After completing this module, I was able to:

- Understand Linux users and groups
- Identify file ownership
- Read Linux permissions
- Modify permissions using chmod
- Change ownership using chown
- Understand sudo privileges
- Read user information from /etc/passwd
- Troubleshoot common permission-related issues

---

# 👥 Linux User Management

Linux is built to support multiple users simultaneously.

Each user has:

- Username
- User ID (UID)
- Primary Group
- Home Directory
- Default Shell

Example:

```
ec2-user:x:1000:1000:EC2 Default User:/home/ec2-user:/bin/bash
```

Breaking it down:

| Field | Meaning |
|---------|----------|
| ec2-user | Username |
| 1000 | User ID (UID) |
| 1000 | Group ID (GID) |
| /home/ec2-user | Home Directory |
| /bin/bash | Default Shell |

This information is stored inside:

```
/etc/passwd
```

---

# 👨‍👩‍👧‍👦 Users and Groups

Every Linux user belongs to one or more groups.

Groups simplify permission management.

Instead of granting permissions to individual users one by one, permissions can be granted to an entire group.

Example:

```
Developers

↓

Alice

Bob

Charlie
```

Instead of configuring permissions for three users individually, Linux allows the group to be assigned the required permissions.

---

# 🔐 Linux Permission Model

Every file and directory has three permission sets.

```
Owner

Group

Others
```

Each permission set contains:

```
Read (r)

Write (w)

Execute (x)
```

Example:

```
-rwxr-xr--
```

Breaking it down:

```
Owner

rwx

↓

Read

Write

Execute
```

```
Group

r-x

↓

Read

Execute
```

```
Others

r--

↓

Read Only
```

---

# Numeric Permission Representation

Linux also represents permissions numerically.

| Permission | Value |
|-------------|------:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Examples:

| Numeric | Meaning |
|----------|----------|
| 777 | Full Access |
| 755 | Owner Full, Others Read & Execute |
| 644 | Owner Read & Write, Others Read |
| 600 | Owner Only |

Understanding these values is essential when configuring application files and scripts.

---

# File Ownership

Every Linux file has:

```
Owner

↓

User
```

and

```
Group
```

Example:

```
-rw-r--r--

ec2-user

ec2-user
```

Meaning:

Owner

↓

ec2-user

Group

↓

ec2-user

---

# Why Ownership Matters

Applications run using specific Linux users.

Examples:

```
nginx

mysql

tomcat

jenkins
```

If the application user does not own the required files or directories, the application may fail with permission errors.

Ownership is therefore a critical aspect of Linux administration.

---

# Administrative Access

Linux separates normal users from administrative users.

Administrative tasks include:

- Installing packages
- Managing users
- Starting services
- Modifying system files
- Mounting filesystems

Instead of logging in directly as the root user, Linux encourages using:

```
sudo
```

This provides temporary administrative privileges while improving system security.

---

# The Root User

The root user is the most privileged account in Linux.

Root can:

- Read any file
- Delete any file
- Modify any configuration
- Manage all users
- Install software
- Stop critical services

Because of this unrestricted access, administrators should use root privileges carefully.

Best practice is to use:

```
sudo
```

only when required.

---

# Understanding /etc/passwd

One of the most important files in Linux is:

```
/etc/passwd
```

It stores information about every user on the system.

Example:

```
ec2-user:x:1000:1000:EC2 Default User:/home/ec2-user:/bin/bash
```

This tells us:

- Username
- UID
- GID
- Description
- Home Directory
- Login Shell

During this phase, we explored this file using:

```
cat /etc/passwd | grep ec2-user
```

and interpreted each field.

---

# Production Scenario 1

## Permission Denied

A developer reports:

> "I cannot write files to the application directory."

Investigation:

```
Check Ownership

↓

Check Permissions

↓

Verify Application User

↓

Correct Ownership

↓

Verify
```

Root cause often involves incorrect ownership or insufficient write permissions.

---

# Production Scenario 2

## AWS EBS Lab

During the AWS EBS storage lab, a new filesystem was mounted successfully.

However, creating a file inside the mount point resulted in:

```
Permission denied
```

Investigation showed that the mounted filesystem was owned by:

```
root

root
```

Since the logged-in user was:

```
ec2-user
```

the user lacked write permissions.

The issue was resolved by changing ownership to the appropriate user.

This was an excellent example of a real-world Linux permission issue.

---

# AWS Relation

Linux permissions are used extensively on AWS.

Examples include:

- EC2 SSH access
- Application deployments
- Log directories
- Mounted EBS volumes
- Nginx document root
- Jenkins workspace
- Docker volumes

Understanding Linux ownership directly impacts application reliability in cloud environments.

---

# Best Practices

✅ Follow the principle of least privilege.

Grant only the permissions required.

---

✅ Prefer changing ownership over granting world-writable permissions.

Avoid:

```
chmod 777
```

unless absolutely necessary.

---

✅ Use groups whenever multiple users require similar access.

---

✅ Use sudo instead of logging in as root.

---

✅ Verify ownership before troubleshooting application failures.

---

# Interview Tips

### Question

What is the difference between a User ID (UID) and a Group ID (GID)?

Expected Answer:

UID uniquely identifies a user, while GID identifies the user's primary group.

---

### Question

What information is stored in /etc/passwd?

Expected Answer:

Username, UID, GID, user description, home directory, and login shell.

---

### Question

Why should chmod 777 be avoided?

Expected Answer:

Because it grants read, write, and execute permissions to everyone, creating a significant security risk.

---

### Question

What is the difference between root and sudo?

Expected Answer:

Root is the superuser account, whereas sudo temporarily grants administrative privileges to authorized users.

---

### Question

Your application reports "Permission denied." What would you check first?

Expected Answer:

- File ownership
- File permissions
- Application user
- Parent directory permissions

---

# Module Summary

This module introduced one of the most important security concepts in Linux—users, groups, ownership, and permissions.

Key skills gained include:

- Understanding Linux users and groups
- Reading permission structures
- Understanding file ownership
- Using administrative privileges safely
- Investigating permission-related issues
- Applying Linux security best practices

These concepts are fundamental to administering Linux servers securely and are encountered daily in Cloud and DevOps environments.