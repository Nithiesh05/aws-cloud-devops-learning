# Module 7 – Archive & Compression Commands

---

# tar

## Purpose

`tar` (Tape Archive) is used to combine multiple files and directories into a single archive file. It can also extract archived files.

> **Note:** `tar` only creates an archive. It does **not** compress files unless used with compression options like `-z` (gzip) or `-j` (bzip2).

---

## Syntax

```bash
tar [options] <archive-name> <files/directories>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-c` | Create a new archive |
| `-x` | Extract an archive |
| `-v` | Verbose output |
| `-f` | Specify archive filename |
| `-t` | List archive contents |
| `-z` | Compress or extract using gzip |
| `-j` | Compress or extract using bzip2 |
| `-C` | Extract to a specific directory |

---

## Examples

Create a tar archive

```bash
tar -cvf backup.tar /etc/nginx
```

Extract an archive

```bash
tar -xvf backup.tar
```

List archive contents

```bash
tar -tvf backup.tar
```

Create a compressed tar archive

```bash
tar -czvf backup.tar.gz /etc/nginx
```

Extract a compressed archive

```bash
tar -xzvf backup.tar.gz
```

Extract to another directory

```bash
tar -xzvf backup.tar.gz -C /opt/backup
```

---

## Sample Output

```text
/etc/nginx/
/etc/nginx/nginx.conf
/etc/nginx/conf.d/
```

---

## Notes

- `-cvf` is the most common option for creating archives.
- `-xvf` is the most common option for extraction.
- Widely used for backups before software upgrades.

---

# gzip

## Purpose

Compresses a file using the Gzip compression algorithm.

Unlike `tar`, `gzip` compresses **only one file at a time**.

---

## Syntax

```bash
gzip [options] <file>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-k` | Keep the original file |
| `-d` | Decompress a file |
| `-v` | Verbose output |
| `-1` | Fastest compression |
| `-9` | Best compression |

---

## Examples

Compress a file

```bash
gzip backup.tar
```

Compress and keep original

```bash
gzip -k backup.tar
```

Maximum compression

```bash
gzip -9 backup.tar
```

---

## Sample Output

```text
backup.tar.gz
```

---

## Notes

- Produces `.gz` files.
- Frequently used after creating a tar archive.
- Does not archive directories.

---

# gunzip

## Purpose

Decompresses files compressed using `gzip`.

---

## Syntax

```bash
gunzip <file.gz>
```

---

## Examples

Extract a gzip file

```bash
gunzip backup.tar.gz
```

Keep the compressed file

```bash
gunzip -k backup.tar.gz
```

---

## Sample Output

```text
backup.tar
```

---

## Notes

- Restores the original file.
- Equivalent to:

```bash
gzip -d backup.tar.gz
```

---

# zip

## Purpose

Creates compressed ZIP archives.

Unlike `tar`, `zip` performs **archiving and compression in a single command**.

---

## Syntax

```bash
zip [options] <archive-name> <files/directories>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-r` | Include directories recursively |
| `-9` | Maximum compression |
| `-q` | Quiet mode |
| `-m` | Move files into archive |

---

## Examples

Compress one file

```bash
zip backup.zip notes.txt
```

Compress multiple files

```bash
zip documents.zip file1.txt file2.txt
```

Compress a directory

```bash
zip -r nginx-backup.zip /etc/nginx
```

Maximum compression

```bash
zip -9 logs.zip logs.txt
```

---

## Sample Output

```text
adding: notes.txt (stored 0%)
```

---

## Notes

- Very common when sharing files between Linux and Windows systems.
- Produces `.zip` archives.

---

# unzip

## Purpose

Extracts ZIP archives.

---

## Syntax

```bash
unzip [options] <archive.zip>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-l` | List archive contents |
| `-d` | Extract to a directory |
| `-o` | Overwrite existing files |
| `-q` | Quiet mode |

---

## Examples

Extract archive

```bash
unzip deployment.zip
```

List archive contents

```bash
unzip -l deployment.zip
```

Extract to another directory

```bash
unzip deployment.zip -d /opt/application
```

Overwrite existing files

```bash
unzip -o deployment.zip
```

---

## Sample Output

```text
inflating: index.html
inflating: app.py
inflating: config.yml
```

---

## Notes

- Creates directories automatically if they exist in the archive.
- Commonly used for deployment packages.

---

# Archive Format Comparison

| Format | Archive | Compression | Multiple Files | Common Usage |
|----------|:-------:|:-----------:|:--------------:|--------------|
| `.tar` | ✅ | ❌ | ✅ | Linux backups |
| `.tar.gz` | ✅ | ✅ | ✅ | Production backups |
| `.gz` | ❌ | ✅ | ❌ | Compress a single file |
| `.zip` | ✅ | ✅ | ✅ | Cross-platform file sharing |

---

# Quick Revision Table

| Command | Purpose |
|----------|----------|
| `tar -cvf` | Create an archive |
| `tar -xvf` | Extract an archive |
| `tar -tvf` | List archive contents |
| `tar -czvf` | Create compressed tar archive |
| `tar -xzvf` | Extract compressed tar archive |
| `gzip` | Compress a file |
| `gzip -k` | Compress and keep original |
| `gunzip` | Decompress a gzip file |
| `zip` | Create ZIP archive |
| `zip -r` | Compress a directory |
| `unzip` | Extract ZIP archive |
| `unzip -l` | List ZIP contents |
| `unzip -d` | Extract to a specific directory |

---