# Terminal Cheat Sheet

> One-page reference for the most common terminal commands.

---

## Navigation

| Task | PowerShell | Bash |
|------|------------|------|
| Current directory | `pwd` | `pwd` |
| Change directory | `cd path` | `cd path` |
| Home directory | `cd ~` | `cd ~` |
| Up one level | `cd ..` | `cd ..` |
| Previous directory | `cd -` | `cd -` |
| List files | `ls` / `Get-ChildItem` | `ls` |
| List all files | `ls -Force` / `Get-ChildItem -Force` | `ls -la` |

## File Operations

| Task | PowerShell | Bash |
|------|------------|------|
| Create file | `New-Item file` / `echo "x" > file` | `touch file` |
| Create directory | `New-Item -ItemType Dir -Path dir` | `mkdir dir` |
| Create nested dirs | `mkdir -Force a\b\c` | `mkdir -p a/b/c` |
| Copy file | `Copy-Item src dest` | `cp src dest` |
| Copy directory | `Copy-Item src dest -Recurse` | `cp -r src dest` |
| Move/rename | `Move-Item old new` | `mv old new` |
| Delete file | `Remove-Item file` | `rm file` |
| Delete directory | `Remove-Item -Recurse dir` | `rm -r dir` |

## Reading Files

| Task | PowerShell | Bash |
|------|------------|------|
| Read file | `cat file` / `Get-Content file` | `cat file` |
| First 10 lines | `Get-Content file -Head 10` | `head -n 10 file` |
| Last 10 lines | `Get-Content file -Tail 10` | `tail -n 10 file` |
| Watch file | `Get-Content file -Wait` | `tail -f file` |
| Count lines | `(cat file).Count` | `wc -l file` |

## Searching

| Task | PowerShell | Bash |
|------|------------|------|
| Find text in file | `Select-String "pattern" file` | `grep "pattern" file` |
| Search recursively | `Get-ChildItem -Recurse \| Select-String "p"` | `grep -r "pattern" .` |
| Find file by name | `Get-ChildItem -Recurse -Filter "*.py"` | `find . -name "*.py"` |
| Find file (modern) | | `fd "*.py"` |
| Search content (fast) | | `rg "pattern"` |

## Text Processing

| Task | PowerShell | Bash |
|------|------------|------|
| Sort | `Sort-Object` | `sort` |
| Unique | `Unique` | `sort \| uniq` |
| Count occurrences | `Group-Object \| Sort Count` | `sort \| uniq -c \| sort -rn` |
| Select column | | `cut -d',' -f1` |
| Replace text | `-replace 'old','new'` | `sed 's/old/new/g'` |
| Print column | | `awk '{print $1}'` |

## Pipes & Redirection

| Operator | PowerShell | Bash | Description |
|----------|------------|------|-------------|
| Pipe | `\|` | `\|` | Send output to next command |
| Write to file | `>` | `>` | Overwrite file |
| Append to file | `>>` | `>>` | Append to file |
| Read from file | `<` | `<` | Input from file |
| Discard output | `> $null` | `> /dev/null` | Throw away output |
| Save and display | `Tee-Object file` | `tee file` | |

## Processes

| Task | PowerShell | Bash |
|------|------------|------|
| List processes | `Get-Process` | `ps aux` |
| Kill by PID | `Stop-Process -Id PID` | `kill PID` |
| Kill by name | `Stop-Process -Name "name"` | `killall name` |
| Force kill | `Stop-Process -Id PID -Force` | `kill -9 PID` |
| Interactive top | `Get-Process \| Sort CPU -Desc` | `top` / `htop` |
| Background job | `Start-Job { script }` | `command &` |
| List jobs | `Get-Job` | `jobs` |

## Networking

| Task | PowerShell | Bash |
|------|------------|------|
| Ping | `Test-Connection host` | `ping host` |
| HTTP GET | `Invoke-WebRequest url` | `curl url` |
| Download file | `Invoke-WebRequest -OutFile f url` | `curl -O url` |
| Check port | `Test-NetConnection host -Port 80` | `nc -zv host 80` |
| DNS lookup | `Resolve-DnsName host` | `nslookup host` |
| IP address | `Get-NetIPAddress` | `ip addr` |

## SSH

| Task | Command |
|------|---------|
| Connect | `ssh user@host` |
| Generate key | `ssh-keygen -t ed25519` |
| Copy key to server | `ssh-copy-id user@host` |
| Copy file to server | `scp file user@host:/path/` |
| Copy file from server | `scp user@host:/path/file .` |

## Environment Variables

| Task | PowerShell | Bash |
|------|------------|------|
| Read variable | `$env:VAR` | `echo $VAR` |
| Set variable | `$env:VAR = "val"` | `export VAR="val"` |
| List all | `Get-ChildItem Env:` | `env` |
| Add to PATH | `$env:PATH += ";new"` | `export PATH="$PATH:new"` |

## Keyboard Shortcuts

| Shortcut | PowerShell | Bash | Description |
|----------|------------|------|-------------|
| Tab | Tab | Tab | Auto-complete |
| Ctrl+C | Ctrl+C | Ctrl+C | Cancel current command |
| Ctrl+Z | | Ctrl+Z | Suspend to background |
| Ctrl+R | F8 | Ctrl+R | Search command history |
| Ctrl+A | Home | Ctrl+A | Move to start of line |
| Ctrl+E | End | Ctrl+E | Move to end of line |
| Ctrl+L | | Ctrl+L | Clear screen |
| Up Arrow | Up | Up | Previous command |
| Down Arrow | Down | Down | Next command |

---

> **Full details:** [Terminal Section](../02-terminal/README.md) | **Next:** [Git Cheat Sheet](../03-git/git-cheat-sheet.md)
