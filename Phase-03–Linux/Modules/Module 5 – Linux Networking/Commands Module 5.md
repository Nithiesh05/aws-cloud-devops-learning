# Module 5 – Linux Networking Commands

---

# hostname

## Purpose

Displays or sets the system's hostname.

---

## Syntax

```bash
hostname
```

---

## Options

| Option | Description |
|---------|-------------|
| `-I` | Display all IP addresses |
| `-f` | Display Fully Qualified Domain Name (FQDN) |
| `-i` | Display IP address of hostname |

---

## Examples

Display hostname

```bash
hostname
```

Output

```text
ip-172-31-49-170
```

Display IP address

```bash
hostname -I
```

Output

```text
172.31.49.170
```

---

## Notes

- Displays the machine name.
- Frequently used after SSH into Linux servers.

---

# hostnamectl

## Purpose

Displays and modifies system hostname information.

---

## Syntax

```bash
hostnamectl
```

---

## Examples

View hostname information

```bash
hostnamectl
```

Change hostname

```bash
sudo hostnamectl set-hostname web-server
```

---

## Sample Output

```text
Static hostname: web-server
Operating System: Amazon Linux 2023
Kernel: Linux 6.x
Architecture: x86_64
```

---

## Notes

- Uses systemd.
- Changes persist after reboot.

---

# ip

## Purpose

Displays and manages network interfaces, IP addresses, and routing information.

---

## Syntax

```bash
ip <object> <command>
```

---

## Common Commands

| Command | Description |
|----------|-------------|
| `ip a` | Show all interfaces |
| `ip addr` | Display IP addresses |
| `ip link` | Show network interfaces |
| `ip route` | Show routing table |

---

## Examples

Display interfaces

```bash
ip a
```

Display routing table

```bash
ip route
```

Display interface information

```bash
ip link
```

---

## Sample Output

```text
2: enX0:
inet 172.31.49.170/20
```

---

## Notes

- Replaces the older `ifconfig` command.
- One of the most frequently used networking commands.

---

# ping

## Purpose

Tests network connectivity between two systems using ICMP.

---

## Syntax

```bash
ping <host>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-c` | Number of packets |
| `-i` | Interval between packets |

---

## Examples

Ping Google

```bash
ping google.com
```

Send four packets

```bash
ping -c 4 google.com
```

Ping an IP address

```bash
ping 8.8.8.8
```

---

## Sample Output

```text
64 bytes from google.com:
time=18 ms
```

---

## Notes

- Uses ICMP packets.
- Verifies connectivity only.
- Does not verify application availability.

---

# curl

## Purpose

Transfers data to or from a server.

Commonly used to test web applications and APIs.

---

## Syntax

```bash
curl <URL>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-I` | Show HTTP headers only |
| `-O` | Download file |
| `-v` | Verbose output |
| `-L` | Follow redirects |

---

## Examples

Test website

```bash
curl http://localhost
```

View HTTP headers

```bash
curl -I google.com
```

Verbose output

```bash
curl -v google.com
```

---

## Sample Output

```text
HTTP/1.1 200 OK
```

---

## Notes

- Used to verify if an application is responding.
- Very common for API testing.

---

# wget

## Purpose

Downloads files from the Internet.

---

## Syntax

```bash
wget <URL>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-c` | Resume download |
| `-O` | Save with another filename |
| `-q` | Quiet mode |

---

## Examples

Download file

```bash
wget https://example.com/file.zip
```

Resume download

```bash
wget -c https://example.com/file.iso
```

Save using another filename

```bash
wget -O backup.zip https://example.com/file.zip
```

---

## Notes

- Useful for downloading packages and scripts.
- Supports download resume.

---

# ss

## Purpose

Displays socket statistics and network connections.

---

## Syntax

```bash
ss [options]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-t` | TCP connections |
| `-u` | UDP connections |
| `-l` | Listening sockets |
| `-n` | Numeric output |
| `-p` | Show process information |

---

## Examples

Show listening ports

```bash
ss -tuln
```

Show listening ports with processes

```bash
ss -tulnp
```

Check port 80

```bash
ss -tulnp | grep 80
```

---

## Sample Output

```text
tcp LISTEN 0 511 0.0.0.0:80
```

---

## Notes

- Replaces the older `netstat` command.
- Frequently used to verify application ports.

---

# nslookup

## Purpose

Queries DNS servers to resolve domain names and IP addresses.

---

## Syntax

```bash
nslookup <domain-or-ip>
```

---

## Examples

Resolve a domain

```bash
nslookup google.com
```

Reverse lookup

```bash
nslookup 8.8.8.8
```

---

## Sample Output

```text
Name: google.com
Address: 142.251.163.100
```

---

## Notes

- Useful for DNS troubleshooting.
- Can perform forward and reverse lookups.

---

# traceroute

## Purpose

Displays the path packets take to reach a destination.

---

## Syntax

```bash
traceroute <host>
```

---

## Examples

Trace Google

```bash
traceroute google.com
```

Trace an IP

```bash
traceroute 8.8.8.8
```

---

## Sample Output

```text
1 240.64.x.x
2 100.100.x.x
3 *
4 *
5 142.251.x.x
```

---

## Notes

- Each line represents one network hop.
- Some routers intentionally do not respond.

---

# nc (Netcat)

## Purpose

Tests TCP or UDP connectivity to specific ports.

---

## Syntax

```bash
nc [options] <host> <port>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-z` | Zero-I/O mode (port scan) |
| `-v` | Verbose output |
| `-u` | UDP mode |

---

## Examples

Check HTTP port

```bash
nc -zv google.com 80
```

Check SSH port

```bash
nc -zv localhost 22
```

---

## Sample Output

```text
Connection to google.com 80 port [tcp/http] succeeded!
```

---

## Notes

- Not installed by default on all Linux distributions.
- Excellent for testing application ports.

---

# Quick Revision Table

| Command | Purpose |
|---------|----------|
| `hostname` | Display system hostname |
| `hostnamectl` | Manage hostname |
| `ip` | Display network configuration |
| `ping` | Test connectivity |
| `curl` | Test web applications and APIs |
| `wget` | Download files |
| `ss` | Display network sockets |
| `nslookup` | DNS lookup |
| `traceroute` | Display packet path |
| `nc` | Test specific ports |

---