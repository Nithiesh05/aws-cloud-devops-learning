# Module 6 – Package Management Commands

---

# dnf

## Purpose

`dnf` (Dandified YUM) is the default package manager in Amazon Linux 2023. It is used to install, update, search, remove, and manage software packages from configured repositories.

---

## Syntax

```bash
dnf <command> [package-name]
```

---

## Common Commands

| Command | Description |
|----------|-------------|
| `dnf install` | Install a package |
| `dnf remove` | Remove a package |
| `dnf update` | Update installed packages |
| `dnf upgrade` | Upgrade the system |
| `dnf search` | Search for packages |
| `dnf info` | Display package information |
| `dnf list installed` | List installed packages |
| `dnf repolist` | Show enabled repositories |
| `dnf clean all` | Clear cached packages |
| `dnf check-update` | Check available updates |

---

## Examples

Search for a package

```bash
dnf search nginx
```

Install a package

```bash
sudo dnf install nginx
```

Install without confirmation

```bash
sudo dnf install nginx -y
```

Remove a package

```bash
sudo dnf remove nginx
```

Update all installed packages

```bash
sudo dnf update
```

Update a specific package

```bash
sudo dnf update nginx
```

Display package information

```bash
dnf info nginx
```

List installed packages

```bash
dnf list installed
```

Show repositories

```bash
dnf repolist
```

Check available updates

```bash
dnf check-update
```

Clear cache

```bash
sudo dnf clean all
```

---

## Sample Output

```text
Last metadata expiration check: 0:15:22 ago.

Installed Packages

nginx.x86_64
Version : 1.26.3
Release : 1.amzn2023
```

---

## Notes

- Automatically installs required dependencies.
- Downloads packages from configured repositories.
- Recommended package manager for Amazon Linux 2023.
- Requires `sudo` for package installation and removal.

---

# rpm

## Purpose

`rpm` (RPM Package Manager) is used to install, verify, query, and remove local RPM packages.

Unlike `dnf`, RPM does **not** automatically resolve package dependencies.

---

## Syntax

```bash
rpm [options] <package.rpm>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-i` | Install package |
| `-U` | Upgrade package |
| `-e` | Remove package |
| `-q` | Query package |
| `-qa` | List all installed RPM packages |
| `-qi` | Display package information |
| `-ql` | List files installed by a package |
| `-ivh` | Install with verbose output and progress |

---

## Examples

Install a local RPM

```bash
sudo rpm -ivh security-agent.rpm
```

Upgrade a package

```bash
sudo rpm -Uvh security-agent.rpm
```

Remove a package

```bash
sudo rpm -e nginx
```

Check if package is installed

```bash
rpm -q nginx
```

View package information

```bash
rpm -qi nginx
```

List installed files

```bash
rpm -ql nginx
```

List all installed RPM packages

```bash
rpm -qa
```

---

## Sample Output

```text
Preparing...

Installing...

security-agent-1.0-1.x86_64
```

---

## Notes

- Does **not** install dependencies automatically.
- Primarily used for locally downloaded RPM files.
- Vendor software is often distributed as RPM packages.

---

# dnf vs rpm

| Feature | DNF | RPM |
|----------|-----|-----|
| Install Packages | ✅ | ✅ |
| Dependency Resolution | ✅ Automatic | ❌ Manual |
| Repository Support | ✅ | ❌ |
| Software Updates | ✅ | Limited |
| Search Packages | ✅ | ❌ |
| Recommended for Daily Use | ✅ | ❌ |

---

# Quick Revision Table

| Command | Purpose |
|----------|----------|
| `dnf install` | Install a package |
| `dnf remove` | Remove a package |
| `dnf update` | Update installed packages |
| `dnf upgrade` | Upgrade the operating system |
| `dnf search` | Search repositories |
| `dnf info` | Display package details |
| `dnf list installed` | Show installed packages |
| `dnf repolist` | Display enabled repositories |
| `dnf check-update` | Check available updates |
| `dnf clean all` | Clear package cache |
| `rpm -ivh` | Install a local RPM package |
| `rpm -Uvh` | Upgrade an RPM package |
| `rpm -e` | Remove an RPM package |
| `rpm -q` | Check if a package is installed |
| `rpm -qi` | View package information |
| `rpm -ql` | List files installed by a package |
| `rpm -qa` | List all installed RPM packages |

---