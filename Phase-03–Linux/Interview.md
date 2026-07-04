# INTERVIEW.md

# Phase 3 – Linux Interview Questions & Answers

---

# Part 1 – Linux Fundamentals, Filesystem, Users & Permissions

---

# Section 1 – Linux Fundamentals

## Q1. What is Linux?

### Answer

Linux is an open-source Unix-like operating system kernel developed by Linus Torvalds in 1991. It manages hardware resources such as CPU, memory, storage, networking, and processes, while allowing users and applications to interact with the system.

Popular Linux distributions include:

- Ubuntu
- Red Hat Enterprise Linux (RHEL)
- CentOS
- Rocky Linux
- Debian
- Amazon Linux

Linux is widely used in servers, cloud platforms, containers, and embedded systems due to its stability, security, and flexibility.

---

## Q2. Why is Linux widely used in Cloud Computing?

### Answer

Linux is preferred because it provides:

- High stability
- Strong security
- Better performance
- Low resource consumption
- Automation support
- Open-source flexibility
- Excellent networking capabilities

Most AWS EC2, Azure VMs, Google Cloud VMs, Docker containers, and Kubernetes nodes run Linux.

---

## Q3. What are the major components of Linux?

### Answer

Linux consists of:

- Kernel
- Shell
- File System
- System Libraries
- Utilities
- User Applications

The kernel is the core component responsible for managing hardware resources.

---

## Q4. What is the difference between Linux Kernel and Operating System?

### Answer

The Kernel is the core component responsible for managing hardware resources.

The Operating System consists of:

- Kernel
- Shell
- Utilities
- Libraries
- User Applications

Linux itself refers to the kernel, while distributions such as Ubuntu or Amazon Linux package the kernel together with user-space software.

---

## Q5. Explain the Linux boot process.

### Answer

The Linux boot sequence is:

```
Power On

↓

BIOS / UEFI

↓

Boot Loader (GRUB)

↓

Linux Kernel

↓

systemd (init)

↓

Services

↓

Login Prompt
```

---

# Section 2 – Linux Filesystem

---

## Q6. What is a Linux filesystem?

### Answer

A filesystem defines how data is organized and stored on a storage device.

Without a filesystem, Linux cannot store files even if a disk is attached.

Common filesystems include:

- XFS
- ext4
- Btrfs

---

## Q7. Explain the Linux directory structure.

### Answer

Some important directories are:

| Directory | Purpose |
|------------|----------|
| / | Root directory |
| /home | User home directories |
| /etc | Configuration files |
| /var | Logs and variable data |
| /usr | Installed applications |
| /opt | Third-party software |
| /tmp | Temporary files |
| /dev | Device files |
| /boot | Boot files |

---

## Q8. What is the difference between an absolute path and a relative path?

### Answer

Absolute Path

- Starts from the root directory (/)
- Example:

```text
/etc/nginx/nginx.conf
```

Relative Path

- Starts from the current working directory

Example

```text
documents/report.txt
```

---

## Q9. What is the difference between pwd and ls?

### Answer

pwd displays the current working directory.

Example

```bash
pwd
```

Output

```
/home/ec2-user
```

ls displays files and directories inside the current directory.

---

## Q10. What is the difference between cp and mv?

### Answer

cp copies files while keeping the original.

mv moves or renames files.

---

## Q11. What is the difference between cat and less?

### Answer

cat displays the entire file immediately.

less displays one page at a time and supports searching.

For large log files, less is preferred.

---

## Q12. Explain grep.

### Answer

grep searches for text patterns inside files.

Example

```bash
grep error application.log
```

Useful for searching logs.

---

## Q13. Explain find.

### Answer

find searches recursively for files and directories.

Example

```bash
find /var -name "*.log"
```

---

# Section 3 – Users & Permissions

---

## Q14. What is the difference between a user and a group?

### Answer

A user represents an individual account.

A group is a collection of users sharing common permissions.

Groups simplify permission management.

---

## Q15. Explain Linux file permissions.

### Answer

Linux permissions are divided into:

```
Owner

Group

Others
```

Each category has:

```
Read (r)

Write (w)

Execute (x)
```

---

## Q16. Explain chmod.

### Answer

chmod changes file permissions.

Example

```bash
chmod 755 script.sh
```

Permission breakdown

```
Owner

rwx

Group

r-x

Others

r-x
```

---

## Q17. Explain chown.

### Answer

chown changes the ownership of files or directories.

Example

```bash
sudo chown ec2-user:ec2-user /data
```

---

## Q18. What does chmod 777 mean?

### Answer

777 grants:

```
Owner

Read

Write

Execute

Group

Read

Write

Execute

Others

Read

Write

Execute
```

Although it provides full access, it is considered insecure and should generally be avoided in production.

---

## Q19. Explain chmod 755.

### Answer

755 means:

Owner

```
rwx
```

Group

```
r-x
```

Others

```
r-x
```

Commonly used for scripts and executable directories.

---

## Q20. Explain chmod 644.

### Answer

644 means:

Owner

```
rw-
```

Group

```
r--
```

Others

```
r--
```

Commonly used for configuration files and documents.

---

## Q21. What is sudo?

### Answer

sudo allows a normal user to execute commands with administrative privileges without logging in directly as the root user.

Example

```bash
sudo dnf install nginx
```

---

## Q22. What is the root user?

### Answer

The root user is the Linux superuser.

It has unrestricted access to all files, services, and system resources.

---

## Q23. Why should we avoid logging in as root?

### Answer

Because accidental commands executed as root can modify or delete critical system files.

Instead, use:

```bash
sudo
```

only when administrative privileges are required.

---

# Scenario-Based Questions

---

## Q24. You receive a "Permission denied" error while writing to a directory. How would you troubleshoot?

### Answer

Investigation steps:

1. Check current user.

```bash
whoami
```

2. Check permissions.

```bash
ls -ld directory
```

3. Check ownership.

```bash
stat directory
```

4. Verify the user has write permission.

5. If ownership is incorrect:

```bash
sudo chown
```

6. If permissions are insufficient:

```bash
chmod
```

---

## Q25. A script is not executing even though it exists. What could be the reason?

### Answer

Possible causes:

- Missing execute permission.
- Wrong interpreter (shebang).
- Incorrect ownership.
- Corrupted file.

First verify:

```bash
ls -l script.sh
```

If execute permission is missing:

```bash
chmod +x script.sh
```

---

## Q26. You accidentally deleted an important file using rm. Can Linux recover it?

### Answer

Normally, no.

Unlike Windows, Linux does not move deleted files to a recycle bin.

Recovery may require specialized recovery tools and is not guaranteed.

Therefore, backups are critical.

---

## Q27. A developer says they cannot edit a configuration file. How would you investigate?

### Answer

Steps:

1. Verify ownership.

```bash
ls -l
```

2. Verify permissions.

3. Check current user.

```bash
whoami
```

4. Verify group membership.

```bash
groups
```

5. Modify ownership or permissions if required.

---

## Q28. What are the most frequently used Linux commands in your daily work?

### Answer

Some commonly used commands include:

- pwd
- ls
- cd
- cp
- mv
- rm
- cat
- grep
- find
- chmod
- chown
- sudo
- stat
- id
- whoami

These commands are used for navigation, file management, permission management, and troubleshooting.

---
# Part 2 – Processes, Services, Logs & Troubleshooting

---

# Section 4 – Processes & Services

---

## Q29. What is a process?

### Answer

A process is a running instance of a program.

Examples:

- NGINX
- Docker
- Jenkins
- MySQL
- SSH
- Python
- Java

Every running process is assigned a unique Process ID (PID) by the Linux kernel.

---

## Q30. What is a Process ID (PID)?

### Answer

A PID (Process ID) is a unique number assigned to every running process.

Linux uses the PID to:

- Monitor processes
- Terminate processes
- Allocate resources
- Track process execution

Example

```bash
ps -ef
```

Output

```text
UID      PID  PPID CMD
root    1250     1 nginx
```

Here,

```
1250
```

is the PID.

---

## Q31. What is the difference between a process and a service?

### Answer

| Process | Service |
|----------|----------|
| Running program | Managed application |
| Has a PID | Managed by systemd |
| Can terminate anytime | Usually runs continuously |
| Temporary | Long-running |

Example:

NGINX Service

↓

Creates multiple worker processes.

---

## Q32. What is systemd?

### Answer

systemd is the default service manager used in modern Linux distributions.

It is responsible for:

- Starting services
- Stopping services
- Restarting services
- Enabling services during boot
- Managing dependencies
- Collecting service logs

---

## Q33. What is systemctl?

### Answer

systemctl is the command-line utility used to manage services controlled by systemd.

Common operations include:

```bash
systemctl status nginx
```

```bash
systemctl start nginx
```

```bash
systemctl stop nginx
```

```bash
systemctl restart nginx
```

```bash
systemctl enable nginx
```

---

## Q34. Difference between start, stop, restart, reload, enable and disable?

### Answer

**start**

Starts a stopped service.

---

**stop**

Stops a running service.

---

**restart**

Stops and starts the service again.

---

**reload**

Reloads the configuration without completely restarting the service.

---

**enable**

Starts the service automatically during system boot.

---

**disable**

Prevents the service from starting automatically during boot.

---

## Q35. Explain the output of systemctl status.

### Answer

Typical output contains:

- Service name
- Loaded status
- Active status
- Main PID
- Recent log messages

Example

```text
Loaded: loaded

Active: active (running)

Main PID: 1456
```

---

## Q36. What is the difference between kill and pkill?

### Answer

**kill**

Terminates a process using its PID.

Example

```bash
kill 1456
```

---

**pkill**

Terminates a process using its name.

Example

```bash
pkill nginx
```

---

## Q37. What is the difference between kill and kill -9?

### Answer

**kill**

Sends SIGTERM (15).

Allows the application to terminate gracefully.

---

**kill -9**

Sends SIGKILL (9).

Immediately terminates the process without allowing cleanup.

Use only when the process does not respond to a normal kill.

---

## Q38. What command do you use to monitor processes in real time?

### Answer

```bash
top
```

or

```bash
htop
```

(if installed)

These commands display:

- CPU usage
- Memory usage
- Running processes
- Process IDs
- Load average

---

# Section 5 – Logs & Troubleshooting

---

## Q39. Why are logs important?

### Answer

Logs record important events occurring on the system.

They help administrators investigate:

- Service failures
- Login attempts
- Hardware detection
- Kernel events
- Application errors
- Security incidents

Logs provide evidence during troubleshooting.

---

## Q40. Where are Linux logs stored?

### Answer

Most Linux logs are stored under:

```text
/var/log
```

Common examples:

```text
/var/log/messages

/var/log/secure

/var/log/boot.log
```

---

## Q41. What is journalctl?

### Answer

journalctl displays logs collected by systemd.

Examples:

View all logs

```bash
journalctl
```

View logs for nginx

```bash
journalctl -u nginx
```

Follow logs

```bash
journalctl -f
```

---

## Q42. What is dmesg?

### Answer

dmesg displays Linux kernel messages.

It is commonly used to troubleshoot:

- Disk detection
- Driver issues
- Hardware
- USB devices
- Boot messages

Example

```bash
dmesg | grep xvdb
```

---

## Q43. Why would you check dmesg after attaching an EBS volume?

### Answer

To verify that the Linux kernel has detected the newly attached storage device.

If the disk appears in the kernel logs, Linux has recognized the hardware successfully.

---

## Q44. Difference between journalctl and dmesg?

### Answer

| journalctl | dmesg |
|-------------|-------|
| Service logs | Kernel logs |
| Application events | Hardware events |
| systemd | Linux kernel |

---

## Q45. What should you check before restarting a failed service?

### Answer

1. Service status

```bash
systemctl status
```

2. Service logs

```bash
journalctl -u
```

3. Process

```bash
ps -ef
```

4. Listening ports

```bash
ss -tulnp
```

Restarting without investigation may temporarily hide the root cause.

---

# Scenario-Based Questions

---

## Q46. A website is down. How would you troubleshoot?

### Answer

I would follow a structured approach:

Step 1

Check whether the server is reachable.

```bash
ping
```

---

Step 2

Verify DNS.

```bash
nslookup
```

---

Step 3

Check whether the web service is running.

```bash
systemctl status nginx
```

---

Step 4

Verify the process.

```bash
ps -ef | grep nginx
```

---

Step 5

Check whether port 80 is listening.

```bash
ss -tulnp | grep 80
```

---

Step 6

Test locally.

```bash
curl localhost
```

---

Step 7

Check logs.

```bash
journalctl -u nginx
```

---

Step 8

Apply the fix and verify.

---

## Q47. NGINX is not starting. What would you investigate?

### Answer

Possible causes:

- Port already in use
- Invalid configuration
- Missing permissions
- Service failure

Investigation:

```bash
systemctl status nginx
```

```bash
journalctl -u nginx
```

```bash
ss -tulnp
```

```bash
ps -ef
```

---

## Q48. High CPU utilization is reported on a Linux server. What would you do?

### Answer

1. Check CPU usage

```bash
top
```

2. Identify high CPU process

3. Find the PID

```bash
ps -ef
```

4. Determine whether the process is expected

5. If necessary, restart the application or terminate the process gracefully

---

## Q49. A service is running, but users still cannot access the application.

### Answer

Possible causes include:

- Firewall rules
- Security Group
- DNS issue
- Wrong port
- Reverse proxy issue
- Application configuration error

Investigation:

- Verify service
- Verify listening port
- Verify connectivity
- Test locally
- Review logs

---

## Q50. You accidentally killed an important production process. What should you do?

### Answer

1. Do not panic.

2. Identify the affected application.

3. Restart the service using:

```bash
systemctl restart
```

4. Verify application functionality.

5. Review logs to ensure normal startup.

6. Inform the team if the incident impacted production.

---

## Q51. A process is consuming 100% CPU. Would you immediately use kill -9?

### Answer

No.

I would first:

- Identify the process.
- Understand why CPU usage is high.
- Check logs.
- Determine whether it is a legitimate workload.

If the process becomes unresponsive and cannot be terminated normally, only then would I use:

```bash
kill -9
```

---

## Q52. How do you troubleshoot a service that repeatedly crashes?

### Answer

My approach would be:

1. Check service status

2. Review logs

3. Identify recent configuration changes

4. Verify permissions

5. Verify disk space

6. Verify memory usage

7. Restart the service after identifying the root cause

---

## Q53. Explain your troubleshooting methodology.

### Answer

I follow a structured process:

```
Understand the Problem

↓

Collect Information

↓

Verify Service

↓

Check Process

↓

Review Logs

↓

Verify Network

↓

Verify Storage

↓

Identify Root Cause

↓

Apply Fix

↓

Validate Solution

↓

Document Learning
```

This minimizes guesswork and ensures that the actual cause of the issue is addressed.

---

# Quick Revision

### Processes

- Process
- PID
- ps
- top
- kill
- pkill

---

### Services

- systemd
- systemctl
- start
- stop
- restart
- reload
- enable
- disable

---

### Logs

- /var/log
- journalctl
- dmesg

---

### Troubleshooting Workflow

```
Problem

↓

Service

↓

Process

↓

Logs

↓

Network

↓

Storage

↓

Root Cause

↓

Fix

↓

Verify
```

---

# Part 3 – Linux Networking

---

# Section 6 – Linux Networking

---

## Q54. What is networking?

### Answer

Networking is the process of connecting two or more devices so they can communicate and exchange data.

In Linux, networking allows servers to:

- Communicate with other servers
- Access the Internet
- Serve web applications
- Connect to databases
- Transfer files
- Resolve domain names

Networking is one of the core components of Cloud Computing.

---

## Q55. What is an IP Address?

### Answer

An IP (Internet Protocol) Address is a unique identifier assigned to a device on a network.

It enables devices to locate and communicate with each other.

Example:

```
172.31.49.170
```

There are two versions:

- IPv4
- IPv6

---

## Q56. What is the difference between Public IP and Private IP?

### Answer

### Public IP

- Accessible from the Internet
- Globally unique
- Used to access servers remotely

Example:

```
52.x.x.x
```

---

### Private IP

- Used inside private networks
- Not directly accessible from the Internet

Example:

```
172.31.x.x
```

AWS EC2 instances usually communicate internally using private IP addresses.

---

## Q57. What is DNS?

### Answer

DNS (Domain Name System) converts human-readable domain names into IP addresses.

Example:

```
google.com

↓

142.250.x.x
```

Without DNS, users would need to remember IP addresses instead of domain names.

---

## Q58. What is the difference between hostname and IP address?

### Answer

Hostname

- Human-readable name
- Easier to remember

Example

```
web-server
```

IP Address

- Numerical network address

Example

```
172.31.49.170
```

DNS maps hostnames to IP addresses.

---

## Q59. Explain the hostname command.

### Answer

The `hostname` command displays the current system hostname.

Example:

```bash
hostname
```

Output

```text
ip-172-31-49-170
```

It is useful for identifying the current machine.

---

## Q60. What is hostnamectl?

### Answer

`hostnamectl` is used to display or change the hostname of a Linux system.

Example

```bash
hostnamectl
```

Change hostname

```bash
sudo hostnamectl set-hostname web-server
```

Unlike the `hostname` command, the change is persistent across reboots.

---

## Q61. What is the ip command?

### Answer

The `ip` command is used to display and configure networking information.

Examples

Display interfaces

```bash
ip a
```

Display routes

```bash
ip route
```

Display interface information

```bash
ip link
```

It replaces the older `ifconfig` command.

---

## Q62. What is ping?

### Answer

`ping` tests network connectivity using ICMP packets.

Example

```bash
ping google.com
```

Successful replies indicate that the destination is reachable.

---

## Q63. Does ping verify that an application is working?

### Answer

No.

`ping` only verifies network connectivity.

A server may respond to ping even if the application running on it has failed.

To verify an application, use:

```bash
curl
```

---

## Q64. What is curl?

### Answer

`curl` is used to communicate with web servers and APIs.

Example

```bash
curl http://localhost
```

It is commonly used to verify whether an application is responding.

---

## Q65. Difference between ping and curl?

### Answer

| ping | curl |
|------|------|
| Tests network connectivity | Tests web application |
| Uses ICMP | Uses HTTP/HTTPS |
| Does not verify application | Verifies application response |

Example

```
ping

↓

Server Reachable

curl

↓

Application Responding
```

---

## Q66. What is wget?

### Answer

`wget` downloads files from remote servers.

Example

```bash
wget https://example.com/file.zip
```

It is commonly used for downloading software packages and installation files.

---

## Q67. Difference between curl and wget?

### Answer

### curl

- Primarily used for testing APIs and web applications
- Can send GET, POST, PUT, DELETE requests
- Displays responses

### wget

- Primarily used to download files
- Supports resuming interrupted downloads

---

## Q68. What is ss?

### Answer

`ss` displays socket statistics and network connections.

Common usage:

```bash
ss -tulnp
```

It shows:

- Listening ports
- Established connections
- Associated processes

---

## Q69. How do you check whether port 80 is listening?

### Answer

```bash
ss -tulnp | grep 80
```

If output appears, the port is in use.

If no output appears, nothing is listening on that port.

---

## Q70. What is nc (Netcat)?

### Answer

`nc` (Netcat) is used to test TCP and UDP connectivity.

Example

```bash
nc -zv google.com 80
```

Common options:

- `-z` → Zero-I/O mode
- `-v` → Verbose output

Note: Netcat may not be installed by default on all Linux distributions.

---

## Q71. What is nslookup?

### Answer

`nslookup` queries DNS servers.

Example

```bash
nslookup google.com
```

It verifies whether DNS resolution is working correctly.

---

## Q72. What is traceroute?

### Answer

`traceroute` displays the path that packets take to reach a destination.

Example

```bash
traceroute google.com
```

Each line represents one network hop.

It helps identify where network communication is failing.

---

# Scenario-Based Questions

---

## Q73. A user says the website is not opening. How would you troubleshoot?

### Answer

My approach would be:

```
Step 1

Check connectivity

↓

ping

↓

Step 2

Verify DNS

↓

nslookup

↓

Step 3

Verify service

↓

systemctl status nginx

↓

Step 4

Verify listening port

↓

ss -tulnp | grep 80

↓

Step 5

Test locally

↓

curl localhost

↓

Step 6

Check logs

↓

journalctl -u nginx
```

This systematic approach helps isolate whether the issue is related to networking, DNS, the web server, or the application itself.

---

## Q74. Ping works, but curl fails. What does this indicate?

### Answer

This indicates that:

- The server is reachable over the network.
- The application or web service may not be running.
- The service may not be listening on the expected port.
- A firewall or reverse proxy configuration could be blocking HTTP traffic.

---

## Q75. curl works on localhost but not from another machine. What could be the issue?

### Answer

Possible causes:

- Firewall blocking traffic
- AWS Security Group does not allow the required port
- NACL restrictions
- Service listening only on `127.0.0.1`
- Incorrect routing

The application itself is working because it responds locally.

---

## Q76. How would you troubleshoot a DNS issue?

### Answer

Steps:

1. Check whether the network is reachable.

```bash
ping 8.8.8.8
```

2. Verify DNS resolution.

```bash
nslookup google.com
```

3. Check DNS configuration.

```bash
cat /etc/resolv.conf
```

4. Verify Internet connectivity.

---

## Q77. A developer says the application is listening on port 8080, but users cannot access it. What would you check?

### Answer

I would verify:

- Application is running

```bash
systemctl status
```

- Port is listening

```bash
ss -tulnp | grep 8080
```

- Local access

```bash
curl localhost:8080
```

- Firewall configuration

- AWS Security Group

- Network ACLs

- Load Balancer configuration (if applicable)

---

## Q78. You SSH into an EC2 instance but cannot access the hosted website. Why?

### Answer

Possible reasons include:

- NGINX or Apache not running
- Port 80/443 not listening
- Security Group blocking inbound traffic
- Firewall blocking HTTP/HTTPS
- Application failure
- Reverse proxy configuration issue

I would verify the service, listening ports, logs, and AWS networking configuration.

---

# Quick Revision

### Basic Commands

- hostname
- hostnamectl
- ip
- ping

---

### Application Testing

- curl
- wget

---

### Port Testing

- ss
- nc

---

### DNS

- nslookup

---

### Network Path

- traceroute

---

### Troubleshooting Flow

```
Cannot Access Website

↓

ping

↓

nslookup

↓

systemctl status

↓

ss -tulnp

↓

curl localhost

↓

journalctl

↓

AWS Security Group

↓

Firewall

↓

Application Configuration
```

---

# Part 4 – Package Management, Archives & Compression

---

# Section 7 – Package Management

---

## Q79. What is a Package Manager?

### Answer

A package manager is a software tool used to install, update, upgrade, remove, and manage software packages on a Linux system.

It automates software management by downloading packages from repositories and resolving dependencies.

Examples:

- DNF (Amazon Linux, Fedora, RHEL)
- YUM (Older RHEL/CentOS)
- APT (Ubuntu, Debian)
- Zypper (SUSE)

---

## Q80. Why do we use a Package Manager?

### Answer

Without a package manager, administrators would need to manually:

- Download software
- Install dependencies
- Configure packages
- Update software
- Resolve version conflicts

A package manager automates these tasks, making software management faster and more reliable.

---

## Q81. What is DNF?

### Answer

DNF (Dandified YUM) is the default package manager for Amazon Linux 2023.

It is used to:

- Install software
- Remove software
- Search packages
- Update packages
- Upgrade the operating system
- Manage repositories

Example:

```bash
sudo dnf install nginx
```

---

## Q82. What is the difference between DNF and RPM?

### Answer

| DNF | RPM |
|-----|-----|
| Smart package manager | Package management utility |
| Resolves dependencies automatically | Does not resolve dependencies |
| Downloads packages from repositories | Installs local RPM files |
| Recommended for daily use | Used mainly for local/vendor packages |

Example:

```bash
sudo dnf install nginx
```

vs

```bash
sudo rpm -ivh package.rpm
```

---

## Q83. What is an RPM package?

### Answer

An RPM package is a software package distributed in the `.rpm` format.

It contains:

- Application files
- Configuration files
- Metadata
- Installation scripts

RPM packages are commonly provided by software vendors.

---

## Q84. What is a repository?

### Answer

A repository is a centralized location that stores software packages.

When you run:

```bash
dnf install nginx
```

DNF downloads the package from the configured repository.

Repositories ensure software comes from trusted sources.

---

## Q85. How do you search for a package?

### Answer

```bash
dnf search nginx
```

This searches all enabled repositories for matching packages.

---

## Q86. How do you view package information?

### Answer

```bash
dnf info nginx
```

This displays:

- Version
- Repository
- Description
- Architecture
- Size

---

## Q87. How do you list enabled repositories?

### Answer

```bash
dnf repolist
```

This displays all enabled package repositories.

---

## Q88. Why is RPM installation sometimes unsuccessful?

### Answer

RPM does not automatically install dependencies.

If required libraries are missing, installation may fail.

Using DNF is preferred because it resolves dependencies automatically.

---

# Section 8 – Archives & Compression

---

## Q89. What is archiving?

### Answer

Archiving is the process of combining multiple files and directories into a single file.

Example:

```
Project

↓

project.tar
```

Archiving does not reduce file size.

---

## Q90. What is compression?

### Answer

Compression reduces the size of a file using compression algorithms.

Example:

```
backup.tar

↓

backup.tar.gz
```

Compression helps save storage space and reduces transfer time.

---

## Q91. What is the difference between archiving and compression?

### Answer

| Archiving | Compression |
|------------|-------------|
| Combines files | Reduces file size |
| Uses TAR | Uses Gzip, Bzip2, Zip |
| No size reduction | Smaller file size |

---

## Q92. What is tar?

### Answer

`tar` (Tape Archive) is used to create and extract archive files.

Example:

```bash
tar -cvf backup.tar /etc/nginx
```

Extract:

```bash
tar -xvf backup.tar
```

---

## Q93. Does tar compress files?

### Answer

No.

`tar` only creates an archive.

Compression is achieved using tools such as:

- gzip
- bzip2
- xz

or by using `tar` together with compression options.

---

## Q94. What is gzip?

### Answer

`gzip` compresses a single file.

Example:

```bash
gzip backup.tar
```

Output:

```
backup.tar.gz
```

---

## Q95. Why do we use tar with gzip?

### Answer

Because:

- TAR combines multiple files.
- Gzip compresses the archive.

Together they produce:

```
backup.tar.gz
```

which is ideal for backups and file transfers.

---

## Q96. What is the difference between tar.gz and zip?

### Answer

| tar.gz | zip |
|---------|-----|
| Archive + compression (two-step process) | Archive and compression in one command |
| Common on Linux | Cross-platform |
| Better for Linux backups | Better for sharing files |

---

## Q97. What is unzip?

### Answer

`unzip` extracts ZIP archives.

Example:

```bash
unzip deployment.zip
```

Extract to another directory:

```bash
unzip deployment.zip -d /opt/application
```

---

## Q98. Why are archives used in production?

### Answer

Archives are commonly used for:

- Backups
- Application deployment
- Log collection
- Disaster recovery
- Configuration backup
- File migration

They simplify storage and transfer of multiple files.

---

# Scenario-Based Questions

---

## Q99. A vendor provides a software package as an RPM file. How would you install it?

### Answer

I would first try:

```bash
sudo dnf install package.rpm
```

because DNF automatically resolves dependencies.

If DNF is unavailable, I can use:

```bash
sudo rpm -ivh package.rpm
```

while ensuring all required dependencies are installed.

---

## Q100. Before upgrading NGINX, what precaution would you take?

### Answer

I would create a backup of the configuration:

```bash
tar -czvf nginx-backup.tar.gz /etc/nginx
```

This allows me to restore the configuration if the upgrade fails.

---

## Q101. Your team needs to transfer an application with thousands of files to another server. How would you do it?

### Answer

I would:

1. Archive the application directory.

```bash
tar -cvf app.tar application/
```

2. Compress the archive.

```bash
gzip app.tar
```

3. Transfer the compressed file.

4. Extract it on the destination server.

This reduces transfer time and keeps all files together.

---

## Q102. A developer accidentally deleted the original archive after compression. Why did this happen?

### Answer

By default, `gzip` replaces the original file with the compressed version.

To retain the original archive:

```bash
gzip -k backup.tar
```

The `-k` option keeps the original file.

---

## Q103. Your backup archive is 20 GB and takes too long to upload. What would you do?

### Answer

I would:

- Compress the archive using gzip.
- Verify unnecessary files are excluded.
- Consider splitting the archive if required.
- Upload the compressed archive instead of the uncompressed tar file.

Compression reduces upload time and storage consumption.

---

## Q104. Explain a typical backup workflow in Linux.

### Answer

A standard workflow is:

```
Application

↓

Create Archive

↓

Compress Archive

↓

Transfer to Backup Location

↓

Verify Backup

↓

Perform Changes

↓

Restore if Required
```

This ensures data can be recovered if changes fail.

---

# Quick Revision

### Package Management

- Package Manager
- DNF
- RPM
- Repository
- Dependency
- dnf install
- dnf search
- dnf info
- dnf repolist

---

### Archives

- tar
- gzip
- gunzip
- zip
- unzip

---

### Key Concepts

- Archive vs Compression
- DNF vs RPM
- tar vs zip
- Backup Strategy
- Deployment Package
- Disaster Recovery

---

### Backup Workflow

```
Files

↓

Archive

↓

Compress

↓

Store

↓

Verify

↓

Deploy

↓

Restore (if required)
```

---

# Part 5 – Linux Storage Management & AWS EBS

---

# Section 9 – Linux Storage Management

---

## Q105. What is storage in Linux?

### Answer

Storage in Linux refers to the devices and filesystems used to permanently store data.

Examples include:

- HDD
- SSD
- NVMe
- AWS Elastic Block Store (EBS)

Storage is used for:

- Operating System
- Application Files
- Databases
- Logs
- User Data
- Backups

---

## Q106. Explain the difference between a disk, partition, filesystem, and mount point.

### Answer

A **Disk** is the physical or virtual storage device.

Example:

```
AWS EBS Volume
```

A **Partition** divides the disk into logical sections.

A **Filesystem** organizes how files are stored on the disk.

Examples:

- XFS
- EXT4

A **Mount Point** connects the filesystem to the Linux directory structure.

Workflow:

```
Disk

↓

Partition

↓

Filesystem

↓

Mount Point

↓

Application
```

---

## Q107. Can Linux store files directly on a newly attached disk?

### Answer

No.

A newly attached disk is raw storage.

Before Linux can store files, the following steps are required:

1. Detect the disk
2. Create a filesystem
3. Create a mount point
4. Mount the filesystem

Only then can applications use the storage.

---

## Q108. What is a filesystem?

### Answer

A filesystem defines how data is organized and stored on a storage device.

Without a filesystem, Linux cannot read or write files.

Common filesystems include:

- XFS
- EXT4
- Btrfs

---

## Q109. What is a mount point?

### Answer

A mount point is a directory where a filesystem is attached.

Example:

```
Filesystem

↓

/data
```

Applications access storage through the mount point.

---

## Q110. What is the difference between df and du?

### Answer

| df | du |
|----|----|
| Displays filesystem usage | Displays directory/file usage |
| Shows free space | Shows space consumed by folders |
| Capacity planning | Storage investigation |

---

## Q111. When would you use df?

### Answer

Use `df` when checking:

- Available disk space
- Filesystem usage
- Capacity planning
- "No space left on device" errors

Example:

```bash
df -h
```

---

## Q112. When would you use du?

### Answer

Use `du` when identifying which directory or file is consuming disk space.

Example:

```bash
du -sh /var/log
```

---

## Q113. What is lsblk?

### Answer

`lsblk` displays information about block storage devices.

It shows:

- Disks
- Partitions
- Filesystem
- Mount points

Example:

```bash
lsblk
```

---

## Q114. Why do we use blkid?

### Answer

`blkid` displays filesystem information including the UUID.

Example:

```bash
sudo blkid
```

UUIDs are commonly used in `/etc/fstab` because they remain consistent even if device names change after reboot.

---

## Q115. What is UUID?

### Answer

UUID stands for **Universally Unique Identifier**.

Every filesystem receives a unique identifier.

UUID is preferred over device names because:

- Device names can change after reboot.
- UUID remains constant.

---

## Q116. What is mount?

### Answer

The `mount` command attaches a filesystem to the Linux directory structure.

Example:

```bash
sudo mount /dev/xvdb /data
```

After mounting, applications can access the storage through `/data`.

---

## Q117. What is umount?

### Answer

The `umount` command detaches a mounted filesystem.

Example:

```bash
sudo umount /data
```

The filesystem should not be in use when unmounting.

---

## Q118. What is findmnt?

### Answer

`findmnt` displays mounted filesystems in an easy-to-read format.

Example:

```bash
findmnt
```

It is useful for verifying active mount points.

---

## Q119. Why do we use /etc/fstab?

### Answer

`/etc/fstab` is used to configure persistent mounts.

Without an entry in `/etc/fstab`, manually mounted filesystems disappear after reboot.

---

## Q120. Why should mount -a be executed after modifying /etc/fstab?

### Answer

`mount -a` validates the `/etc/fstab` configuration without rebooting.

If there are configuration errors, they can be identified and corrected immediately.

---

# Section 10 – AWS Elastic Block Store (EBS)

---

## Q121. What is Amazon EBS?

### Answer

Amazon Elastic Block Store (EBS) is a block storage service for Amazon EC2.

It provides persistent storage that remains available even after an EC2 instance is stopped.

Common use cases:

- Operating System disks
- Databases
- Application data
- Logs
- Backups

---

## Q122. Can an EBS volume be attached to any EC2 instance?

### Answer

No.

An EBS volume can only be attached to an EC2 instance in the **same Availability Zone (AZ)**.

---

## Q123. Explain the lifecycle of attaching a new EBS volume to an EC2 instance.

### Answer

The workflow is:

```
Create EBS Volume

↓

Attach to EC2

↓

Verify with lsblk

↓

Create Filesystem

↓

Create Mount Point

↓

Mount Filesystem

↓

Verify Mount

↓

Retrieve UUID

↓

Update /etc/fstab

↓

Test with mount -a
```

---

## Q124. Why is creating a filesystem necessary?

### Answer

A new EBS volume contains raw storage.

Linux cannot organize or store files until a filesystem is created.

Example:

```bash
mkfs.xfs /dev/xvdb
```

---

## Q125. Why do we use UUID instead of /dev/xvdb in /etc/fstab?

### Answer

Device names such as `/dev/xvdb` can change after reboot.

UUID remains constant, ensuring the correct filesystem is mounted.

---

# Scenario-Based Questions

---

## Q126. You attached a new EBS volume, but it does not appear in lsblk. What would you investigate?

### Answer

I would check:

1. Whether the volume is attached in the AWS Console.
2. Whether the volume and EC2 instance are in the same Availability Zone.
3. Kernel detection using:

```bash
dmesg
```

4. Re-run:

```bash
lsblk
```

---

## Q127. You mounted a new EBS volume, but creating a file returns "Permission denied". How would you troubleshoot?

### Answer

This is the exact issue we encountered during the lab.

Steps:

1. Verify mount.

```bash
findmnt
```

2. Check ownership.

```bash
ls -ld /data
```

3. Check current user.

```bash
whoami
```

4. If the directory is owned by `root`, update ownership.

```bash
sudo chown -R ec2-user:ec2-user /data
```

5. Verify write access.

---

## Q128. A mounted filesystem disappears after reboot. What is the likely cause?

### Answer

The filesystem was mounted manually but was not configured in `/etc/fstab`.

I would:

1. Retrieve the UUID.

```bash
blkid
```

2. Add the UUID to `/etc/fstab`.

3. Validate the configuration.

```bash
sudo mount -a
```

---

## Q129. Your EC2 instance reports "No space left on device". How would you troubleshoot?

### Answer

1. Check filesystem usage.

```bash
df -h
```

2. Identify large directories.

```bash
du -sh /*
```

3. Archive or remove unnecessary files.

4. Extend the EBS volume if required.

---

## Q130. You are asked to increase storage for an application without downtime. What would you do?

### Answer

My approach would be:

1. Create a new EBS volume.
2. Attach it to the EC2 instance.
3. Verify detection using `lsblk`.
4. Create a filesystem.
5. Create a mount point.
6. Mount the filesystem.
7. Update `/etc/fstab`.
8. Migrate application data if required.
9. Verify the application.

---

## Q131. Walk me through the EBS lab you completed.

### Answer

During the lab, I:

1. Created a new EBS volume.
2. Attached it to an EC2 instance.
3. Verified the device using `lsblk`.
4. Created an XFS filesystem.
5. Created a mount point (`/data`).
6. Mounted the filesystem.
7. Retrieved the UUID using `blkid`.
8. Configured persistent mounting in `/etc/fstab`.
9. Validated using `mount -a`.
10. Verified using `findmnt`.
11. Encountered a "Permission denied" error due to root ownership.
12. Resolved it using:

```bash
sudo chown -R ec2-user:ec2-user /data
```

13. Successfully created files.
14. Unmounted the filesystem.
15. Detached and deleted the EBS volume.

This lab helped me understand the complete storage provisioning lifecycle in Linux and AWS.

---

# Quick Revision

### Storage

- Disk
- Partition
- Filesystem
- Mount Point
- UUID
- /etc/fstab

---

### Commands

- df
- du
- lsblk
- blkid
- mount
- umount
- findmnt
- mkfs

---

### AWS

- EBS
- Availability Zone
- Persistent Storage
- Filesystem Creation
- Mounting
- UUID
- /etc/fstab

---

### Storage Workflow

```
Create EBS

↓

Attach

↓

lsblk

↓

mkfs

↓

mkdir

↓

mount

↓

blkid

↓

/etc/fstab

↓

mount -a

↓

findmnt

↓

Application Ready
```

---
