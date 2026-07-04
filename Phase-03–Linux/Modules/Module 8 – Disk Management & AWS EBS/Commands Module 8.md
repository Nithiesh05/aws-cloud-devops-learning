# Module 8 – Linux Storage Management Commands

---

# df

## Purpose

Displays the available and used disk space for mounted filesystems.

---

## Syntax

```bash
df [options] [filesystem]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-h` | Human-readable sizes (KB, MB, GB) |
| `-T` | Show filesystem type |
| `-i` | Display inode usage |
| `-a` | Show all filesystems |

---

## Examples

Display disk usage

```bash
df -h
```

Display root filesystem usage

```bash
df -h /
```

Show filesystem type

```bash
df -Th
```

Display inode usage

```bash
df -i
```

---

## Sample Output

```text
Filesystem      Size Used Avail Use% Mounted on
/dev/xvda1      8.0G 1.8G 6.2G 23% /
```

---

## Notes

- Shows filesystem usage, not folder usage.
- One of the first commands to run when a server reports "No space left on device."

---

# du

## Purpose

Displays disk usage for files and directories.

---

## Syntax

```bash
du [options] <directory>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-h` | Human-readable output |
| `-s` | Display summary only |
| `-a` | Show files and directories |
| `-c` | Display grand total |

---

## Examples

Directory size

```bash
du -sh /var/log
```

Home directory size

```bash
du -sh ~
```

Display all folders

```bash
du -sh ~/*
```

Sort folders by size

```bash
du -sh ~/* | sort -h
```

---

## Sample Output

```text
56M /var/log
```

---

## Notes

- Used to identify which directory is consuming disk space.
- Complements the `df` command.

---

# lsblk

## Purpose

Displays information about all block storage devices attached to the system.

---

## Syntax

```bash
lsblk [options]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-f` | Show filesystem information |
| `-o` | Display selected columns |
| `-p` | Show full device paths |

---

## Examples

Display block devices

```bash
lsblk
```

Display filesystem details

```bash
lsblk -f
```

Display selected columns

```bash
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
```

---

## Sample Output

```text
NAME      SIZE TYPE MOUNTPOINT
xvda        8G disk
├─xvda1     8G part /
└─xvda128  10M part /boot/efi
```

---

## Notes

- One of the first commands used after attaching a new AWS EBS volume.
- Helps verify whether Linux has detected the new disk.

---

# blkid

## Purpose

Displays filesystem information such as UUID, filesystem type, and labels.

---

## Syntax

```bash
blkid [device]
```

---

## Examples

Display all block device UUIDs

```bash
sudo blkid
```

Display a specific device

```bash
sudo blkid /dev/xvda1
```

---

## Sample Output

```text
/dev/xvda1: UUID="b3601c2b-2c07-4ade-9cb4-e02157f43c7d" TYPE="xfs"
```

---

## Notes

- UUIDs are commonly used in `/etc/fstab`.
- UUIDs remain the same even if the device name changes after a reboot.

---

# mount

## Purpose

Mounts a filesystem so it becomes accessible through a directory.

---

## Syntax

```bash
mount [device] [mount-point]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-a` | Mount all filesystems in `/etc/fstab` |
| `-t` | Specify filesystem type |
| `-o` | Specify mount options |

---

## Examples

Mount a filesystem

```bash
sudo mount /dev/xvdb /data
```

Mount using filesystem type

```bash
sudo mount -t xfs /dev/xvdb /data
```

Mount all entries from fstab

```bash
sudo mount -a
```

---

## Sample Output

```text
(No output indicates successful mount.)
```

---

## Notes

- Mounting is temporary unless configured in `/etc/fstab`.
- Always verify the mount after executing the command.

---

# umount

## Purpose

Unmounts a mounted filesystem.

---

## Syntax

```bash
umount <device-or-mount-point>
```

---

## Examples

Unmount using mount point

```bash
sudo umount /data
```

Unmount using device

```bash
sudo umount /dev/xvdb
```

---

## Sample Output

```text
(No output indicates successful unmount.)
```

---

## Notes

- Ensure no process is using the filesystem before unmounting.
- Stop applications writing to the disk before detaching storage.

---

# findmnt

## Purpose

Displays mounted filesystems in an easy-to-read format.

---

## Syntax

```bash
findmnt [target]
```

---

## Examples

Display all mounted filesystems

```bash
findmnt
```

Display root mount

```bash
findmnt /
```

Display a device mount

```bash
findmnt /dev/xvda1
```

Display a specific mount point

```bash
findmnt /data
```

---

## Sample Output

```text
TARGET SOURCE     FSTYPE OPTIONS
/      /dev/xvda1 xfs    rw,noatime
```

---

## Notes

- Easier to read than the traditional `mount` output.
- Useful for verifying mount points during troubleshooting.

---

# mkfs

## Purpose

Creates a filesystem on a disk or partition.

---

## Syntax

```bash
mkfs.<filesystem> <device>
```

---

## Examples

Create an XFS filesystem

```bash
sudo mkfs.xfs /dev/xvdb
```

Create an EXT4 filesystem

```bash
sudo mkfs.ext4 /dev/xvdb
```

---

## Sample Output

```text
meta-data=/dev/xvdb
data blocks=262144
```

---

## Notes

- Erases all existing data on the device.
- Should only be executed on a new or empty disk.

---

# mkdir

## Purpose

Creates a directory to be used as a mount point.

---

## Syntax

```bash
mkdir <directory>
```

---

## Examples

Create a mount directory

```bash
sudo mkdir /data
```

Create nested directories

```bash
sudo mkdir -p /mnt/storage
```

---

## Notes

- A mount point must exist before mounting a filesystem.

---

# cat

## Purpose

Displays the contents of configuration files.

---

## Syntax

```bash
cat <file>
```

---

## Examples

View the fstab configuration

```bash
cat /etc/fstab
```

---

## Sample Output

```text
UUID=b3601c2b-2c07-4ade-9cb4-e02157f43c7d /data xfs defaults,nofail 0 2
```

---

## Notes

- Useful for verifying persistent mount configurations.

---

# Quick Revision Table

| Command | Purpose |
|----------|----------|
| `df -h` | Display filesystem usage |
| `du -sh` | Display directory size |
| `lsblk` | Display block devices |
| `lsblk -f` | Display filesystems |
| `blkid` | Display UUID and filesystem information |
| `mkfs.xfs` | Create an XFS filesystem |
| `mount` | Mount a filesystem |
| `mount -a` | Test `/etc/fstab` configuration |
| `umount` | Unmount a filesystem |
| `findmnt` | Display mounted filesystems |
| `mkdir` | Create a mount point |
| `cat /etc/fstab` | View persistent mount configuration |

---

# Storage Provisioning Workflow

```
Create EBS Volume
        │
        ▼
Attach to EC2
        │
        ▼
lsblk
        │
        ▼
mkfs.xfs
        │
        ▼
mkdir /data
        │
        ▼
mount
        │
        ▼
blkid
        │
        ▼
Update /etc/fstab
        │
        ▼
mount -a
        │
        ▼
findmnt
        │
        ▼
Application Uses Storage
```

---