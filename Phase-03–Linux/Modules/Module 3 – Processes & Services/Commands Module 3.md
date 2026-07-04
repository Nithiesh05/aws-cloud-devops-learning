# Module 3 – Processes & Services Commands

---

# ps

## Purpose

Displays information about currently running processes.

---

## Syntax

```bash
ps [options]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-e` | Show all processes |
| `-f` | Full format listing |
| `-u` | Show processes for a user |
| `-ef` | Display all processes in full format |
| `aux` | BSD style output with detailed information |

---

## Examples

View current shell processes

```bash
ps
```

View all running processes

```bash
ps -ef
```

Find NGINX process

```bash
ps -ef | grep nginx
```

Find SSH process

```bash
ps -ef | grep ssh
```

---

## Sample Output

```text
UID        PID  PPID  C STIME TTY      TIME CMD
root      1243     1  0 09:30 ?        00:00:01 nginx
```

---

## Notes

- Every running application has a Process ID (PID).
- Often combined with `grep` to search for specific processes.

---

# top

## Purpose

Displays real-time information about running processes and system resource usage.

---

## Syntax

```bash
top
```

---

## Useful Shortcuts

| Key | Description |
|------|-------------|
| `q` | Quit |
| `P` | Sort by CPU usage |
| `M` | Sort by Memory usage |
| `k` | Kill a process |
| `h` | Help |

---

## Examples

Start monitoring

```bash
top
```

---

## Sample Output

```text
PID USER      CPU% MEM%
1234 nginx     2.5  1.3
1456 mysql    15.2 12.4
```

---

## Notes

- Updates continuously.
- Useful for identifying high CPU or memory consumption.

---

# kill

## Purpose

Terminates a running process using its Process ID (PID).

---

## Syntax

```bash
kill <PID>
```

---

## Common Signals

| Signal | Description |
|---------|-------------|
| `15` | Graceful termination (default) |
| `9` | Force kill |
| `1` | Reload configuration (SIGHUP) |

---

## Examples

Terminate a process

```bash
kill 2456
```

Force terminate

```bash
kill -9 2456
```

---

## Notes

- Use `kill -9` only when a process does not terminate normally.
- Verify the PID before killing a process.

---

# pkill

## Purpose

Terminates processes by process name instead of PID.

---

## Syntax

```bash
pkill <process-name>
```

---

## Examples

Kill all nginx processes

```bash
pkill nginx
```

Kill all python processes

```bash
pkill python
```

---

## Notes

- Easier than finding the PID manually.
- Use carefully, as it can terminate multiple processes.

---

# systemctl

## Purpose

Manages Linux services controlled by systemd.

---

## Syntax

```bash
systemctl <action> <service>
```

---

## Common Actions

| Action | Description |
|---------|-------------|
| `status` | View service status |
| `start` | Start service |
| `stop` | Stop service |
| `restart` | Restart service |
| `reload` | Reload configuration |
| `enable` | Start service at boot |
| `disable` | Disable service at boot |

---

## Examples

Check NGINX status

```bash
sudo systemctl status nginx
```

Start service

```bash
sudo systemctl start nginx
```

Restart service

```bash
sudo systemctl restart nginx
```

Enable service

```bash
sudo systemctl enable nginx
```

Stop service

```bash
sudo systemctl stop nginx
```

---

## Sample Output

```text
● nginx.service - The nginx HTTP Server
   Active: active (running)
```

---

## Notes

- One of the most frequently used commands in Linux administration.
- Works with services managed by systemd.

---

# service

## Purpose

Manages services on older Linux systems.

---

## Syntax

```bash
service <service-name> <action>
```

---

## Examples

Check status

```bash
sudo service nginx status
```

Restart service

```bash
sudo service nginx restart
```

---

## Notes

- Mostly replaced by `systemctl`.
- Still available on some Linux distributions.

---

# journalctl

## Purpose

Displays logs collected by systemd.

---

## Syntax

```bash
journalctl [options]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-u` | View logs for a service |
| `-f` | Follow logs in real time |
| `-n` | Show last N log entries |
| `-b` | Show logs since last boot |

---

## Examples

View all logs

```bash
journalctl
```

View NGINX logs

```bash
journalctl -u nginx
```

Follow logs

```bash
journalctl -f
```

Last 20 entries

```bash
journalctl -n 20
```

---

## Notes

- Primary command for investigating service failures.
- Very useful during troubleshooting.

---

# dmesg

## Purpose

Displays kernel messages.

---

## Syntax

```bash
dmesg
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-T` | Show human-readable timestamps |
| `-H` | Human-readable output |

---

## Examples

View kernel messages

```bash
dmesg
```

Human-readable timestamps

```bash
dmesg -T
```

Search for disk detection

```bash
dmesg | grep xvdb
```

---

## Notes

- Useful for troubleshooting hardware.
- Frequently used after attaching new EBS volumes.

---

# pgrep

## Purpose

Displays the Process ID (PID) of matching processes.

---

## Syntax

```bash
pgrep <process-name>
```

---

## Examples

Find nginx PID

```bash
pgrep nginx
```

Find ssh PID

```bash
pgrep sshd
```

---

## Sample Output

```text
1243
```

---

## Notes

- Returns only the PID.
- Useful when combined with `kill`.

---

# jobs

## Purpose

Displays background jobs running in the current shell.

---

## Syntax

```bash
jobs
```

---

## Examples

View background jobs

```bash
jobs
```

---

## Sample Output

```text
[1]+ Running sleep 100 &
```

---

## Notes

- Shows only jobs started in the current terminal.
- Different from `ps`, which shows system-wide processes.

---

# bg

## Purpose

Resumes a stopped job in the background.

---

## Syntax

```bash
bg %<job-number>
```

---

## Examples

Resume Job 1

```bash
bg %1
```

---

## Notes

- Works with jobs created in the current shell.

---

# fg

## Purpose

Brings a background job to the foreground.

---

## Syntax

```bash
fg %<job-number>
```

---

## Examples

Bring Job 1 to the foreground

```bash
fg %1
```

---

## Notes

- Useful for interacting with paused or background jobs.

---

# nohup

## Purpose

Runs a command that continues even after logging out.

---

## Syntax

```bash
nohup <command> &
```

---

## Examples

Run a script

```bash
nohup python app.py &
```

Run backup

```bash
nohup ./backup.sh &
```

---

## Notes

- Output is stored in `nohup.out` by default.
- Useful for long-running background tasks.

---

# Quick Revision Table

| Command | Purpose |
|---------|----------|
| `ps` | Show running processes |
| `top` | Real-time process monitoring |
| `kill` | Terminate a process using PID |
| `pkill` | Kill processes by name |
| `systemctl` | Manage Linux services |
| `service` | Manage services (legacy) |
| `journalctl` | View systemd logs |
| `dmesg` | View kernel logs |
| `pgrep` | Find PID by process name |
| `jobs` | Show background jobs |
| `bg` | Resume job in background |
| `fg` | Bring job to foreground |
| `nohup` | Run command after logout |

---