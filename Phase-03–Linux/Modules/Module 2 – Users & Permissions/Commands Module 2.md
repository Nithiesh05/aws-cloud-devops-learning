# Module 2 – Users & Permissions Commands

---

# whoami

## Purpose

Displays the username of the currently logged-in user.

---

## Syntax

```bash
whoami
```

---

## Examples

Display current user

```bash
whoami
```

Output

```text
ec2-user
```

---

## Notes

- Useful to verify the current logged-in user.
- Helpful before performing administrative tasks.

---

# id

## Purpose

Displays user and group identity information.

---

## Syntax

```bash
id [username]
```

---

## Examples

Display current user's information

```bash
id
```

Example Output

```text
uid=1000(ec2-user) gid=1000(ec2-user) groups=1000(ec2-user)
```

Display another user's information

```bash
id root
```

---

## Notes

- Shows User ID (UID)
- Shows Group ID (GID)
- Displays all groups the user belongs to

---

# passwd

## Purpose

Changes a user's password.

---

## Syntax

```bash
passwd [username]
```

---

## Examples

Change your password

```bash
passwd
```

Change another user's password (root/sudo)

```bash
sudo passwd ec2-user
```

---

## Notes

- Requires the current password for normal users.
- Requires sudo privileges to change another user's password.

---

# sudo

## Purpose

Executes a command with administrative (root) privileges.

---

## Syntax

```bash
sudo <command>
```

---

## Examples

Install a package

```bash
sudo dnf install nginx
```

Restart a service

```bash
sudo systemctl restart nginx
```

Edit a configuration file

```bash
sudo vi /etc/fstab
```

---

## Notes

- Temporarily grants root privileges.
- Preferred over logging in directly as the root user.

---

# chmod

## Purpose

Changes file or directory permissions.

---

## Syntax

```bash
chmod [options] <permissions> <file>
```

---

## Common Permission Values

| Permission | Meaning |
|------------|---------|
| 777 | Read, Write, Execute for everyone |
| 755 | Owner: Full, Others: Read & Execute |
| 700 | Owner: Full Access |
| 644 | Owner: Read & Write, Others: Read Only |
| 600 | Owner: Read & Write |

---

## Examples

Give execute permission

```bash
chmod +x script.sh
```

Set permission to 755

```bash
chmod 755 script.sh
```

Set permission to 644

```bash
chmod 644 notes.txt
```

---

## Notes

- Numeric permissions are commonly used.
- Avoid using `777` unless absolutely necessary.

---

# chown

## Purpose

Changes the owner of a file or directory.

---

## Syntax

```bash
chown <owner> <file>
```

---

## Examples

Change owner

```bash
sudo chown ec2-user file.txt
```

Change owner and group

```bash
sudo chown ec2-user:ec2-user file.txt
```

Change ownership recursively

```bash
sudo chown -R ec2-user:ec2-user /data
```

---

## Notes

- Frequently used after mounting new filesystems.
- Requires sudo privileges in most cases.

---

# chgrp

## Purpose

Changes the group ownership of a file or directory.

---

## Syntax

```bash
chgrp <group> <file>
```

---

## Examples

Change group

```bash
sudo chgrp developers project.txt
```

Recursive group change

```bash
sudo chgrp -R developers /project
```

---

## Notes

- Only modifies the group ownership.
- Does not change the file owner.

---

# ls -l

## Purpose

Displays detailed file information including permissions and ownership.

---

## Syntax

```bash
ls -l
```

---

## Example

```bash
ls -l
```

Output

```text
-rw-r--r-- 1 ec2-user ec2-user 120 Jul 4 notes.txt
```

---

## Understanding the Output

```text
-rw-r--r--
```

Permission Breakdown

```
Owner

rw-

↓

Read

Write

Group

r--

↓

Read

Others

r--

↓

Read
```

Owner

```text
ec2-user
```

Group

```text
ec2-user
```

File Size

```text
120 Bytes
```

---

## Notes

- One of the most commonly used commands for checking permissions.
- Useful during permission troubleshooting.

---

# groups

## Purpose

Displays the groups a user belongs to.

---

## Syntax

```bash
groups [username]
```

---

## Examples

Display current user's groups

```bash
groups
```

Output

```text
ec2-user wheel docker
```

Display another user's groups

```bash
groups root
```

---

## Notes

- Useful when troubleshooting permission issues.
- Helps verify group memberships.

---

# umask

## Purpose

Displays or sets the default permission mask for newly created files and directories.

---

## Syntax

```bash
umask
```

Set a new umask

```bash
umask 022
```

---

## Examples

View current umask

```bash
umask
```

Output

```text
0022
```

---

## Notes

- Controls default permissions.
- Does not change permissions of existing files.

---

# stat

## Purpose

Displays detailed information about a file or directory.

---

## Syntax

```bash
stat <file>
```

---

## Examples

View file information

```bash
stat notes.txt
```

Example Output

```text
File: notes.txt
Size: 120
Access: (0644/-rw-r--r--)
Uid: (1000/ec2-user)
Gid: (1000/ec2-user)
```

---

## Notes

- Displays timestamps.
- Shows inode information.
- Useful for detailed file inspection.

---