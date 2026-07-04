# Module 8 – Linux Storage Management & AWS Elastic Block Store (EBS)

---

# 📖 Introduction

Storage is one of the most fundamental resources in any computing environment.

Applications require storage to save configuration files, databases, logs, user uploads, backups, and temporary data. Without properly configured storage, applications cannot function reliably.

In Linux, attaching a storage device is only the beginning. Before an application can use the storage, the operating system must recognize the device, a filesystem must be created, the device must be mounted, appropriate permissions must be configured, and the mount should be made persistent across system reboots.

During this module, I learned how Linux manages storage devices and completed a full AWS Elastic Block Store (EBS) provisioning project that closely resembles real-world Cloud Engineer responsibilities.

---

# 🎯 Learning Objectives

After completing this module, I was able to:

- Understand Linux storage architecture
- Differentiate between disks, partitions, filesystems, and mount points
- Monitor disk usage
- Analyze directory storage consumption
- Detect block storage devices
- Create filesystems
- Mount and unmount storage
- Configure persistent mounts
- Understand UUIDs
- Provision and manage AWS EBS volumes
- Troubleshoot storage-related issues

---

# Why Storage Matters

Every production application stores data.

Examples include:

- Web server configuration
- Application logs
- User uploads
- Database files
- Backup archives
- Container volumes

Without reliable storage:

- Applications fail to start.
- Databases become unavailable.
- Logs cannot be written.
- Backups cannot be created.

Storage management is therefore a core responsibility of Linux administrators and Cloud Engineers.

---

# Linux Storage Architecture

```
          Physical / Virtual Disk
                    │
                    ▼
              Partition (Optional)
                    │
                    ▼
              Filesystem (XFS, ext4)
                    │
                    ▼
               Mount Point
                    │
                    ▼
             Linux Directory
                    │
                    ▼
          Applications Read/Write Data
```

Every layer has a specific purpose, and all layers must be correctly configured before applications can use the storage.

---

# Understanding the Storage Components

## Disk

A disk is the physical or virtual storage device attached to a Linux machine.

Examples include:

- HDD
- SSD
- NVMe
- AWS EBS Volume

A newly attached disk is simply raw storage.

Linux cannot store files on it until it is prepared.

---

## Partition

A partition divides a disk into logical sections.

Large disks may contain multiple partitions.

Example:

```
Disk

↓

Partition 1

Partition 2

Partition 3
```

Some Linux systems use partitions, while others use the entire disk directly.

---

## Filesystem

A filesystem defines how data is organized on the storage device.

Common Linux filesystems include:

- XFS
- ext4
- Btrfs

Without a filesystem, Linux has no method to organize files and directories on the disk.

Think of the filesystem as the index of a book—it tells the operating system where every file is located.

---

## Mount Point

A mount point connects the filesystem to the Linux directory structure.

Example:

```
Filesystem

↓

Mounted

↓

/data
```

Once mounted, applications can access the storage by reading and writing to `/data`.

---

# Storage Provisioning Workflow

The complete storage lifecycle followed during this phase is shown below.

```
Create EBS Volume

↓

Attach to EC2

↓

Detect Device

↓

Create Filesystem

↓

Create Mount Point

↓

Mount Filesystem

↓

Verify Mount

↓

Configure /etc/fstab

↓

Test Configuration

↓

Application Uses Storage
```

This workflow represents a common storage provisioning task performed by Cloud Engineers.

---

# Monitoring Storage Usage

One of the most common responsibilities of a Linux administrator is monitoring available storage.

Storage monitoring helps identify:

- Full filesystems
- Capacity planning requirements
- Unexpected storage growth
- Log accumulation
- Backup space requirements

A full filesystem can prevent applications from writing data, creating logs, or even starting correctly.

---

# Understanding Disk Usage vs Directory Usage

During this phase, an important distinction was learned.

## Filesystem Usage

Filesystem usage answers the question:

> **"How full is the disk?"**

This helps determine whether additional storage is required.

---

## Directory Usage

Directory usage answers a different question:

> **"Which directory is consuming the storage?"**

This information is valuable when cleaning up log files or identifying unexpected storage consumption.

Understanding the difference between these two perspectives is an essential troubleshooting skill.

---

# Block Devices

Linux represents storage devices as block devices.

Examples:

```
/dev/xvda

/dev/xvdb
```

When a new EBS volume is attached, Linux detects it as a new block device.

Before using the storage, administrators verify that the operating system has recognized the new device.

---

# UUID (Universally Unique Identifier)

Every filesystem receives a unique identifier called a UUID.

Example:

```
Filesystem

↓

UUID

↓

b3601c2b-2c07-4ade-9cb4-e02157f43c7d
```

Unlike device names, UUIDs remain consistent across reboots.

This makes UUIDs the recommended method for configuring persistent mounts.

---

# Temporary vs Persistent Mounts

A mounted filesystem can exist in two ways.

## Temporary Mount

```
Mount

↓

Available

↓

System Reboots

↓

Mount Disappears
```

Temporary mounts are useful for testing.

---

## Persistent Mount

Persistent mounts survive system reboots.

This is achieved by adding the filesystem to:

```
/etc/fstab
```

Production systems almost always use persistent mounts.

---

# AWS Hands-on Project – EBS Lifecycle

This module concluded with a complete AWS storage administration project.

The project followed the complete lifecycle below.

```
Create EBS Volume

↓

Attach Volume

↓

Verify Device Detection

↓

Create XFS Filesystem

↓

Create Mount Directory

↓

Mount Filesystem

↓

Verify Mount

↓

Retrieve UUID

↓

Configure /etc/fstab

↓

Test Configuration

↓

Reboot Verification

↓

Unmount

↓

Detach Volume

↓

Delete Volume
```

This workflow closely resembles storage provisioning tasks performed by Cloud Engineers in production environments.

---

# Real Production Issue Encountered

During the hands-on lab, the newly mounted filesystem could not be written to.

Attempting to create a file resulted in:

```
Permission denied
```

## Investigation

The filesystem was mounted successfully.

However, the ownership of the mounted directory belonged to:

```
root

↓

root
```

The logged-in user was:

```
ec2-user
```

Since the user did not own the mounted filesystem, write operations failed.

---

## Resolution

Ownership of the mounted directory was updated to the appropriate user.

After correcting the ownership, the filesystem became writable.

---

## Lesson Learned

Mounting a filesystem does **not** automatically grant write access to all users.

After every new storage mount, administrators should verify:

- Ownership
- Permissions
- Application access

This was one of the most valuable real-world lessons from the entire Linux phase.

---

# Production Scenario 1

## Application Requires Additional Storage

```
Application Running Out of Space

↓

Provision New EBS Volume

↓

Attach to EC2

↓

Create Filesystem

↓

Mount

↓

Update Application Configuration

↓

Verify
```

---

# Production Scenario 2

## Filesystem Full

Investigation workflow:

```
Filesystem Full

↓

Check Filesystem Usage

↓

Identify Large Directories

↓

Archive or Remove Unnecessary Data

↓

Verify Available Space
```

---

# Production Scenario 3

## Storage Not Available After Reboot

Investigation:

```
Verify Mount

↓

Check /etc/fstab

↓

Verify UUID

↓

Test Configuration

↓

Reboot Again
```

This highlights the importance of configuring persistent mounts correctly.

---

# AWS Relation

This module directly maps to several AWS services.

| Linux Concept | AWS Service |
|---------------|-------------|
| Disk | Amazon EBS |
| Server | Amazon EC2 |
| Filesystem | XFS / ext4 |
| Mount Point | Linux Directory |
| Persistent Storage | EBS Volume |
| UUID | Persistent Mount Configuration |

Understanding Linux storage is essential for working with EC2 instances, databases, container platforms, and stateful workloads in AWS.

---

# Best Practices

✅ Monitor storage utilization regularly.

---

✅ Always verify that newly attached disks are detected before creating filesystems.

---

✅ Use UUIDs instead of device names in `/etc/fstab`.

---

✅ Test `/etc/fstab` before rebooting.

---

✅ Verify ownership and permissions after mounting storage.

---

✅ Unmount filesystems before detaching storage.

---

✅ Never delete an EBS volume until all required data has been backed up.

---

# Interview Tips

### Question

What is the difference between a disk and a filesystem?

**Expected Answer:**

A disk provides raw storage, while a filesystem organizes data so that Linux can store and retrieve files.

---

### Question

Why do we mount a filesystem?

**Expected Answer:**

Mounting connects the filesystem to the Linux directory structure, allowing applications and users to access the stored data.

---

### Question

Why should UUIDs be used instead of device names?

**Expected Answer:**

Device names may change after a reboot, but UUIDs remain consistent, making them more reliable for persistent mounts.

---

### Question

A mounted EBS volume shows "Permission denied." What would you investigate?

**Expected Answer:**

- Mount status
- Ownership
- File permissions
- Application user
- Filesystem configuration

---

### Question

Why should `mount -a` be executed after modifying `/etc/fstab`?

**Expected Answer:**

It validates the configuration immediately without requiring a reboot, allowing administrators to detect errors before they impact the system.

---

# Key Learnings

This module brought together everything learned throughout Phase 3.

I learned that storage administration is not simply attaching a disk.

A complete storage workflow involves:

```
Provision

↓

Detect

↓

Filesystem

↓

Mount

↓

Permissions

↓

Persistence

↓

Verification

↓

Application Ready
```

I also learned that successful storage management requires careful planning, verification, and testing rather than simply executing commands.

---

# Module Summary

This module introduced Linux storage administration from a practical Cloud Engineering perspective.

Key skills gained include:

- Understanding Linux storage architecture
- Working with disks, filesystems, and mount points
- Monitoring storage utilization
- Managing block devices
- Configuring persistent storage
- Provisioning and managing AWS EBS volumes
- Troubleshooting storage-related issues
- Applying production storage best practices

The AWS EBS project completed during this module provided hands-on experience with the complete storage lifecycle, making it one of the most valuable practical exercises in this Linux learning journey.