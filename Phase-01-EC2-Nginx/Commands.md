# 💻 COMMANDS.md

# Linux & AWS Commands Used in Phase 1

This document contains all the Linux commands used throughout Phase 1 of my Cloud & DevOps learning journey.

Instead of simply listing commands, each section explains:

* What the command does
* Why I used it
* Example usage
* Expected output
* Real-world use case

---

# 1. SSH

## Purpose

Used to securely connect to the EC2 instance from a local machine.

---

## Syntax

```bash
ssh -i key.pem ec2-user@<Public-IP>
```

---

## Why I Used It

To access the Linux server running on AWS EC2 and perform administrative tasks.

---

## Real-World Usage

SSH is commonly used to:

* Configure servers
* Install software
* Troubleshoot issues
* View logs
* Deploy applications

---

# 2. pwd

## Purpose

Displays the current working directory.

---

## Syntax

```bash
pwd
```

---

## Example Output

```text
/home/ec2-user
```

---

## Why I Used It

To verify my current location before editing or creating files.

---

# 3. whoami

## Purpose

Displays the currently logged-in user.

---

## Syntax

```bash
whoami
```

---

## Example Output

```text
ec2-user
```

---

## Why I Used It

To confirm which Linux user I was logged in as.

---

# 4. hostname

## Purpose

Displays the hostname of the machine.

---

## Syntax

```bash
hostname
```

---

## Why I Used It

To verify the identity of the EC2 instance after connecting.

---

# 5. ls -l

## Purpose

Lists files and directories with detailed information.

---

## Syntax

```bash
ls -l
```

---

## Information Displayed

* Permissions
* Owner
* Group
* File Size
* Last Modified Time
* File Name

---

## Why I Used It

To verify that the `index.html` file existed before editing it.

---

# 6. vim

## Purpose

A terminal-based text editor used to create and modify files.

---

## Example

```bash
vim index.html
```

---

## Why I Used It

To replace the default Nginx page with my own HTML webpage.

---

## Important Shortcuts

| Key | Action              |
| --- | ------------------- |
| i   | Insert Mode         |
| ESC | Exit Insert Mode    |
| :w  | Save                |
| :q  | Quit                |
| :wq | Save and Exit       |
| :q! | Exit Without Saving |

---

# 7. systemctl

## Purpose

Manages Linux services using systemd.

---

## Commands Used

Check status

```bash
systemctl status nginx
```

Start service

```bash
sudo systemctl start nginx
```

Restart service

```bash
sudo systemctl restart nginx
```

Reload configuration

```bash
sudo systemctl reload nginx
```

Enable on boot

```bash
sudo systemctl enable nginx
```

---

## Why I Used It

To manage the Nginx web server throughout the project.

---

# 8. nginx -t

## Purpose

Validates the Nginx configuration file.

---

## Syntax

```bash
sudo nginx -t
```

---

## Why I Used It

Before restarting or reloading Nginx to ensure the configuration contained no syntax errors.

---

## Best Practice

Always run:

```bash
nginx -t
```

before:

```bash
systemctl reload nginx
```

---

# 9. ss -tulnp

## Purpose

Displays listening ports and active network sockets.

---

## Syntax

```bash
ss -tulnp
```

---

## Why I Used It

To verify that Nginx was listening on Port 80.

---

## Important Output

```text
0.0.0.0:80
```

Meaning:

Nginx is listening on all IPv4 interfaces.

---

# 10. curl

## Purpose

Sends HTTP requests from the command line.

---

## Syntax

```bash
curl http://localhost
```

---

## Why I Used It

To determine whether the issue was related to:

* Nginx
* AWS Networking

If localhost worked but the browser failed, I knew the issue was outside the web server.

---

# 11. stat

## Purpose

Displays detailed information about a file.

---

## Syntax

```bash
stat index.html
```

---

## Information Displayed

* Size
* Permissions
* Owner
* Last Modified
* Last Accessed
* Inode

---

## Why I Used It

To verify file properties after modifying the webpage.

---

# 12. tail

## Purpose

Displays the last few lines of a file.

---

## Commands Used

Access Log

```bash
sudo tail -10 /var/log/nginx/access.log
```

Error Log

```bash
sudo tail -10 /var/log/nginx/error.log
```

---

## Why I Used It

To inspect recent web requests and identify Nginx-related errors.

---

# 13. journalctl

## Purpose

Displays logs collected by systemd services.

---

## Syntax

```bash
journalctl -u nginx
```

---

## Why I Used It

To troubleshoot the Nginx service and review recent service events.

---

## Example

```bash
journalctl -u nginx --since "10 minutes ago"
```

Shows only logs generated within the last ten minutes.

---

# 14. ip addr

## Purpose

Displays all network interfaces and IP addresses assigned to the Linux machine.

---

## Syntax

```bash
ip addr
```

---

## Why I Used It

To understand the difference between Public IP and Private IP.

I discovered that Linux only displayed the Private IP because AWS handles Public IP translation externally through the Internet Gateway.

---

# 15. ps -ef | grep nginx

## Purpose

Displays running Nginx processes.

---

## Syntax

```bash
ps -ef | grep nginx
```

---

## Why I Used It

To verify whether the Nginx master and worker processes were running.

---

# Troubleshooting Commands

Whenever the website was not accessible, I followed this sequence:

```text
1. systemctl status nginx

↓

2. curl localhost

↓

3. ss -tulnp | grep :80

↓

4. journalctl -u nginx

↓

5. tail /var/log/nginx/error.log

↓

6. Verify Security Group

↓

7. Verify Route Table

↓

8. Verify Internet Gateway
```

---

# Key Commands to Remember

| Command                  | Why It Is Important         |
| ------------------------ | --------------------------- |
| `systemctl status nginx` | Check service health        |
| `curl localhost`         | Verify application locally  |
| `ss -tulnp`              | Check listening ports       |
| `journalctl -u nginx`    | View service logs           |
| `tail -f error.log`      | Monitor errors in real time |
| `ip addr`                | View network interfaces     |
| `nginx -t`               | Validate configuration      |
| `ps -ef`                 | Verify running processes    |

---

# Final Notes

One of the biggest lessons from this project was understanding that commands are not meant to be memorized individually.

Instead, each command serves a specific purpose during troubleshooting.

The goal is to understand **when** to use a command, **why** to use it, and **how** its output helps narrow down the root cause of an issue.
