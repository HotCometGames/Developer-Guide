# The File System

> How files and directories are organized, how paths work across operating systems, and what you need to know about permissions and hidden files.

> **Related:** [Operating Systems](operating-systems.md) | [Environment Variables](environment-variables.md)

---

## What Is It?

The file system is the **organizational structure** that the operating system uses to store and retrieve files on disk.

Every OS has a file system, and the fundamentals are the same everywhere:

- **Files** — named sequences of bytes (a document, a program, an image)
- **Directories** (a.k.a. folders) — containers that hold files and other directories
- **Paths** — addresses that tell the OS where a file or directory lives
- **Permissions** — rules about who can read, write, or execute each file

## Why Does It Exist?

Without a file system, data on a disk would be one giant undifferentiated blob. The file system provides:

- **Organization** — find anything by its path
- **Persistence** — data survives between reboots
- **Sharing** — multiple programs can access the same files
- **Security** — permissions control who can do what

## Mental Model

### The Directory Tree

```text
/ (root)
├── home/          (Linux/macOS user homes)
│   └── user/
│       ├── Documents/
│       └── Projects/
├── Users/         (Windows user homes)
│   └── User/
│       ├── Documents/
│       └── Projects/
├── etc/           (Linux config — no Windows equivalent)
├── Applications/  (macOS apps — no Linux equivalent)
├── Program Files/ (Windows programs — no Linux equivalent)
└── tmp/           (temporary files, cleared on reboot)
```

### Path Types

| Type | Windows | Mac/Linux |
|------|---------|-----------|
| Absolute | `C:\Users\Name\file.txt` | `/home/name/file.txt` |
| Relative | `..\sibling\file.txt` | `../sibling/file.txt` |
| Home | `C:\Users\Name` | `/home/name` |
| Current | `.` | `.` |
| Parent | `..` | `..` |

### Path Separators

```text
Windows: \  (backslash)
Mac/Linux: /  (forward slash)
```

**Universal rule:** In code, always use `/` — every OS accepts it in programming contexts. Or use a path-joining function from the standard library.

### Hidden Files

| OS | Mechanism | Example | Hide/Show |
|----|-----------|---------|-----------|
| Linux/macOS | Name starts with `.` | `.git`, `.env` | `ls -la` to see |
| Windows | Hidden attribute flag | `AppData` | Explorer → View → Hidden items |

Hidden files usually store **configuration** — dotfiles, project settings, temporary data.

## Permissions

### Linux / macOS

| Type | Symbol | Meaning |
|------|--------|---------|
| Read | `r` | View file contents / list directory |
| Write | `w` | Modify file / add or delete files in directory |
| Execute | `x` | Run file as a program / enter directory |

Permissions are set for three roles: **owner**, **group**, and **others**.

```text
-rwxr-xr--  1 user  group  1024 Mar 1 12:00 script.sh
 ^^^^^^^^^
 |||||||||
 ||||||||└─ Others: read only
 |||||||└── Group: read + execute
 ||||||└─── Owner: read + write + execute
 |||||└──── Type: - = file, d = directory, l = symlink
```

### Windows

Windows uses ACLs (Access Control Lists) — more granular but shown through GUI Properties → Security tab. For most dev work, the key distinction is whether the file is **read-only** or not.

## Cheat Sheet

```
Paths:
  Absolute: starts from root (C:\, /)
  Relative: starts from current dir (., ..)

  Cross-platform: always use / in code

Hidden files:
  Linux/Mac: prefix with dot (.)
  Windows: hidden attribute

Permissions (Linux/Mac):
  chmod 755 file  → rwxr-xr-x (owner all, others read+execute)
  chmod 644 file  → rw-r--r-- (owner read+write, others read)
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Hardcoding paths | Works on your machine, breaks everywhere else | Use env vars, config files, or a path library |
| Mixing backslashes and forward slashes | Breaks on non-Windows | Use `/` or `path.join()` / `os.path.join()` |
| Assuming case-insensitivity | Linux paths are case-sensitive — `File.txt` ≠ `file.txt` | Always use consistent casing |
| Editing `.git` directory directly | Corrupts the repository | Use `git` commands only |
| Committing secret files | Leaks API keys, passwords | Add secrets to `.gitignore` and check before committing |
| Not understanding permissions | "Permission denied" errors with no explanation | Run `ls -la` (Linux/Mac) or check Properties → Security (Windows) |

## Related Topics

- [Operating Systems](operating-systems.md) — How each OS organizes its file system
- [Environment Variables](environment-variables.md) — System-wide values that often contain paths
- [The Command Prompt](the-command-prompt.md) — How to navigate the file system from a terminal

## Further Learning

- [Files and File Systems](https://en.wikipedia.org/wiki/File_system) — Wikipedia overview
- *The Linux Programming Interface* — Michael Kerrisk (Chapter on file I/O)
- [Windows File System](https://learn.microsoft.com/en-us/windows/win32/fileio/file-systems) — Microsoft docs

---

> **Next:** [Operating Systems](operating-systems.md) | **Previous:** [How Computers Work](how-computers-work.md)
