# COMMANDS.md

# Phase 3 – Linux Commands Reference

This document contains all the Linux commands covered during **Phase 3**.

Each command includes its purpose, syntax, commonly used options, examples, sample output, and important notes.

---

# Module 1 – Linux Filesystem & Navigation Commands

---

# pwd

## Purpose

Displays the current working directory.

---

## Syntax

```bash
pwd
```

---

## Options

The `pwd` command generally does not require options.

| Option | Description |
|---------|-------------|
| `-P` | Displays the physical directory without symbolic links |
| `-L` | Displays the logical directory (default behavior) |

---

## Examples

Display current directory

```bash
pwd
```

Output

```
/home/ec2-user
```

---

## Notes

- One of the safest commands in Linux.
- Useful before performing file operations.
- Displays the absolute path of the current directory.

---

# ls

## Purpose

Lists files and directories.

---

## Syntax

```bash
ls [options] [directory]
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-l` | Long listing format |
| `-a` | Show hidden files |
| `-h` | Human-readable file sizes |
| `-R` | List recursively |
| `-t` | Sort by modification time |
| `-S` | Sort by file size |

---

## Examples

List files

```bash
ls
```

Long listing

```bash
ls -l
```

Show hidden files

```bash
ls -a
```

Human-readable sizes

```bash
ls -lh
```

List recursively

```bash
ls -R
```

---

## Sample Output

```text
drwxr-xr-x 2 ec2-user ec2-user 4096 Jul 3 Documents
-rw-r--r-- 1 ec2-user ec2-user   52 Jul 3 notes.txt
```

---

## Notes

- Hidden files begin with a `.`
- `ls -lh` is commonly used because file sizes are easier to read.
- `ls -la` is one of the most frequently used combinations.

---

# cd

## Purpose

Changes the current working directory.

---

## Syntax

```bash
cd <directory>
```

---

## Examples

Go to home directory

```bash
cd
```

Go to a specific directory

```bash
cd /etc
```

Go to parent directory

```bash
cd ..
```

Go back to previous directory

```bash
cd -
```

Go to root directory

```bash
cd /
```

---

## Sample Output

```text
/home/ec2-user
```

After

```bash
cd /etc
```

Running

```bash
pwd
```

returns

```text
/etc
```

---

## Notes

- `cd` without arguments always returns to the user's home directory.
- `cd -` switches to the previous working directory.

---

# mkdir

## Purpose

Creates new directories.

---

## Syntax

```bash
mkdir [options] <directory-name>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-p` | Creates parent directories if they do not exist |
| `-v` | Displays a message for each directory created |

---

## Examples

Create a directory

```bash
mkdir project
```

Create multiple directories

```bash
mkdir dev test prod
```

Create nested directories

```bash
mkdir -p project/backend/logs
```

---

## Sample Output

```text
project/
```

---

## Notes

- `mkdir -p` is useful when creating nested directory structures.
- Existing directories are not recreated when using `-p`.

---

# rmdir

## Purpose

Removes empty directories.

---

## Syntax

```bash
rmdir <directory-name>
```

---

## Options

| Option | Description |
|---------|-------------|
| `-p` | Removes parent directories if they become empty |
| `-v` | Displays detailed output |

---

## Examples

Remove an empty directory

```bash
rmdir project
```

Remove nested empty directories

```bash
rmdir -p project/backend/logs
```

---

## Notes

- Only removes empty directories.
- To remove directories containing files, use `rm -r`.

---

# touch

## Purpose

Creates empty files or updates file timestamps.

---

## Syntax

```bash
touch <file-name>
```

---

## Examples

Create one file

```bash
touch file.txt
```

Create multiple files

```bash
touch file1.txt file2.txt file3.txt
```

Update timestamp

```bash
touch file.txt
```

---

## Sample Output

```
file.txt
```

---

## Notes

- If the file exists, only its timestamp is updated.
- If it does not exist, an empty file is created.

---

# cp

## Purpose

Copies files and directories.

---

## Syntax

```bash
cp [options] <source> <destination>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-r` | Copy directories recursively |
| `-v` | Verbose output |
| `-i` | Confirm before overwrite |
| `-p` | Preserve permissions and timestamps |

---

## Examples

Copy a file

```bash
cp file1.txt backup.txt
```

Copy a directory

```bash
cp -r project backup
```

Verbose copy

```bash
cp -rv project backup
```

---

## Notes

- `cp -r` is required for directories.
- Existing files may be overwritten unless `-i` is used.

---

# mv

## Purpose

Moves or renames files and directories.

---

## Syntax

```bash
mv <source> <destination>
```

---

## Examples

Rename a file

```bash
mv old.txt new.txt
```

Move a file

```bash
mv notes.txt Documents/
```

Move a directory

```bash
mv project /opt/
```

---

## Notes

- No separate rename command exists in Linux.
- `mv` is used for both moving and renaming.

---

# rm

## Purpose

Deletes files and directories.

---

## Syntax

```bash
rm [options] <file>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-r` | Remove directories recursively |
| `-f` | Force removal |
| `-i` | Confirm before deletion |
| `-v` | Verbose output |

---

## Examples

Delete a file

```bash
rm file.txt
```

Delete a directory

```bash
rm -r project
```

Force delete

```bash
rm -rf project
```

---

## Notes

- Deleted files cannot be recovered easily.
- Use `rm -rf` with extreme caution.

---

# cat

## Purpose

Displays the contents of a file.

---

## Syntax

```bash
cat <file-name>
```

---

## Examples

View a file

```bash
cat notes.txt
```

View multiple files

```bash
cat file1.txt file2.txt
```

Create a file

```bash
cat > notes.txt
```

---

## Notes

- Suitable for small files.
- Large files are better viewed using `less`.

---

# less

## Purpose

Views large files one page at a time.

---

## Syntax

```bash
less <file-name>
```

---

## Useful Shortcuts

| Key | Description |
|------|-------------|
| `/` | Search |
| `n` | Next search result |
| `Space` | Next page |
| `b` | Previous page |
| `q` | Quit |

---

## Example

```bash
less /var/log/messages
```

---

## Notes

- Preferred over `cat` for large files.
- Supports searching within files.

---

# head

## Purpose

Displays the beginning of a file.

---

## Syntax

```bash
head [options] <file-name>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-n` | Display specified number of lines |

---

## Examples

First 10 lines

```bash
head file.txt
```

First 20 lines

```bash
head -20 file.txt
```

---

## Notes

- Default output is the first 10 lines.

---

# tail

## Purpose

Displays the end of a file.

---

## Syntax

```bash
tail [options] <file-name>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-n` | Number of lines |
| `-f` | Follow file changes in real time |

---

## Examples

Last 10 lines

```bash
tail file.txt
```

Real-time log monitoring

```bash
tail -f /var/log/messages
```

---

## Notes

- `tail -f` is commonly used for monitoring log files.

---

# find

## Purpose

Searches for files and directories.

---

## Syntax

```bash
find <path> [options]
```

---

## Examples

Find a file

```bash
find /home -name notes.txt
```

Find all text files

```bash
find /home -name "*.txt"
```

Find directories

```bash
find /etc -type d
```

---

## Notes

- Searches recursively.
- One of the most powerful Linux commands.

---

# grep

## Purpose

Searches for text patterns inside files.

---

## Syntax

```bash
grep [options] <pattern> <file>
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `-i` | Ignore case |
| `-n` | Show line numbers |
| `-r` | Recursive search |
| `-v` | Invert match |

---

## Examples

Search for "error"

```bash
grep error logfile.txt
```

Ignore case

```bash
grep -i error logfile.txt
```

Recursive search

```bash
grep -r nginx /etc
```

---

## Sample Output

```text
25:error starting nginx
```

---

## Notes

- Extremely useful for log analysis.
- Frequently combined with other Linux commands using pipes (`|`).

---

