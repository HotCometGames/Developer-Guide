# Terminal Troubleshooting

> Common terminal errors and how to fix them. Find your error, get the solution.

---

## What Is This Page?

A quick-reference for the most common terminal problems. Find the error message you're seeing and get the fix.

## Common Errors by Category

### "Command Not Found" / "Command Not Recognized"

| Problem | Cause | Solution |
|---------|-------|----------|
| `'git' is not recognized` | Git not installed or not in PATH | Install Git, restart terminal |
| `'node' is not recognized` | Node.js not installed or not in PATH | Install Node.js, restart terminal |
| `'python' is not recognized` | Python not installed or not in PATH | Install Python, add to PATH |
| `'docker' is not recognized` | Docker not installed | Install Docker Desktop |
| `'command' is not recognized` | Command not in PATH | Install the tool or add to PATH |

**Fix PATH on Windows:**
```powershell
# Check current PATH
$env:PATH -split ';'

# Add to PATH (user level)
$currentPath = [Environment]::GetEnvironmentVariable("PATH", "User")
[Environment]::SetEnvironmentVariable("PATH", "$currentPath;C:\new\path", "User")

# Restart terminal
```

**Fix PATH on Linux/macOS:**
```bash
# Check current PATH
echo $PATH

# Add to PATH (add to ~/.bashrc)
export PATH="$PATH:/new/path"
source ~/.bashrc
```

### "Permission Denied"

| Problem | Cause | Solution |
|---------|-------|----------|
| `Permission denied (publickey)` | SSH key not installed | Run `ssh-copy-id` |
| `Permission denied` on file | No write permission | Use `chmod` or `sudo` |
| `EACCES` (npm/yarn) | Permission issue with node_modules | Fix npm permissions |
| `Cannot execute` | Script not executable | Run `chmod +x script.sh` |

**Fix file permissions:**
```bash
# Make script executable
chmod +x script.sh

# Make directory writable
chmod -R u+w directory/
```

**Fix npm permissions (Linux):**
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### "No Such File or Directory"

| Problem | Cause | Solution |
|---------|-------|----------|
| `No such file or directory` | Wrong path | Check with `ls` / `dir` |
| `cd: no such file or directory` | Directory doesn't exist | Create it first with `mkdir` |
| `cat: file: No such file` | File doesn't exist | Check filename and path |

**Debug:**
```bash
# Check if file exists
ls -la /path/to/file

# Check if directory exists
ls -la /path/to/directory/

# Check current directory
pwd
```

### "Access Denied" / "UnauthorizedAccess"

| Problem | Cause | Solution |
|---------|-------|----------|
| PowerShell execution policy | Scripts blocked by default | `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| `403 Forbidden` (web) | Server rejecting request | Check authentication/permissions |
| `EACCES` (npm) | Permission issue | Fix npm directory permissions |

**Fix PowerShell execution policy:**
```powershell
# Check current policy
Get-ExecutionPolicy

# Set to RemoteSigned (allows local scripts)
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Network Errors

| Problem | Cause | Solution |
|---------|-------|----------|
| `Connection refused` | Service not running on target port | Start the service |
| `Connection timed out` | Firewall or network issue | Check firewall rules |
| `Could not resolve host` | DNS failure | Try `8.8.8.8` as DNS |
| `SSL certificate problem` | Expired or invalid certificate | Use `-k` for testing only |
| `404 Not Found` | Wrong URL | Check the URL |

**Debug network:**
```bash
# Test basic connectivity
ping google.com

# Test DNS resolution
nslookup example.com

# Test specific port
nc -zv localhost 3000

# Verbose curl
curl -v https://example.com
```

### Git Errors

| Problem | Cause | Solution |
|---------|-------|----------|
| `fatal: not a git repository` | Not in a git repo | `git init` or `cd` to repo |
| `error: failed to push some refs` | Remote has changes you don't | `git pull --rebase` first |
| `fatal: refusing to merge` | Uncommitted changes | Commit or stash first |
| `error: pathspec 'branch' did not match` | Branch doesn't exist | `git branch -a` to list |
| `fatal: remote origin already exists` | Remote URL already set | `git remote set-url origin URL` |

### Python/Conda Errors

| Problem | Cause | Solution |
|---------|-------|----------|
| `pip: command not found` | Python not in PATH | Reinstall Python, check PATH |
| `conda: command not found` | Conda not initialized | Run `conda init bash` |
| `python: command not found` | Try `python3` | Use `python3` on Linux/macOS |
| `ModuleNotFoundError` | Package not installed | `pip install package` |
| `No module named 'pip'` | pip not installed | `python -m ensurepip` |

### Node.js/npm Errors

| Problem | Cause | Solution |
|---------|-------|----------|
| `npm: command not found` | Node.js not installed | Install Node.js |
| `EACCES permission denied` | npm directory permission issue | Fix npm prefix |
| `peer dependency` warnings | Version conflicts | Use `--legacy-peer-deps` |
| `ENOSPC: System limit` | Linux inotify limit | `echo fs.inotify.max_user_watches=524288 \| sudo tee -a /etc/sysctl.conf` |

## PowerShell-Specific Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Scripts won't execute | Execution policy | `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| `.\script.ps1` doesn't work | Need `.\` prefix | Use `.\script.ps1` not `script.ps1` |
| `ConvertFrom-Json` fails | Input isn't valid JSON | Validate JSON first |
| Pipeline output is text | Using `Write-Host` | Use `Write-Output` instead |

## Bash-Specific Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| `#!/bin/bash` not found | Wrong shebang | Use `#!/usr/bin/env bash` |
| `unary operator expected` | Empty variable in test | Quote: `"$var"` |
| `too many arguments` | Unquoted glob expanded | Quote patterns |
| `syntax error near unexpected token` | Windows line endings | `dos2unix script.sh` |

## Quick Diagnosis Commands

```bash
# What shell am I using?
echo $SHELL

# What's in my PATH?
echo $PATH | tr ':' '\n'

# Where is a command?
which git
where git  # Windows

# What version?
git --version
node --version
python --version

# Am I in a git repo?
git status
```

```powershell
# PowerShell equivalents
$PSVersionTable.PSVersion
$env:PATH -split ';'
Get-Command git
git status
```

## When All Else Fails

1. **Google the exact error message** - Someone else has had this problem
2. **Check the documentation** - Official docs for the tool
3. **Try a different terminal** - Rule out terminal-specific issues
4. **Restart the terminal** - Clears stuck state
5. **Restart the computer** - Nuclear option, but effective

## Related Topics

- [What Is a Terminal?](what-is-a-terminal.md) - Terminal fundamentals
- [Environment Variables](environment-variables.md) - PATH issues
- [PowerShell vs Bash](powershell-vs-bash.md) - Shell differences

---

## Personal Notes

> Add your own notes about errors you've encountered and their solutions.
