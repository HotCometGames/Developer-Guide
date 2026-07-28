# Terminal Quick Reference

> One-page command reference for the terminal. Print this or bookmark it.

---

## Navigation

| Task | PowerShell | Bash |
|------|------------|------|
| Current path | `pwd` | `pwd` |
| Change dir | `cd path` | `cd path` |
| Home | `cd ~` | `cd ~` |
| Up one level | `cd ..` | `cd ..` |
| Previous dir | `cd -` | `cd -` |
| List files | `Get-ChildItem` | `ls` |
| List all | `Get-ChildItem -Force` | `ls -la` |

## Files

| Task | PowerShell | Bash |
|------|------------|------|
| Create file | `New-Item file` | `touch file` |
| Create dir | `New-Item -ItemType Dir -Path d` | `mkdir d` |
| Nested dirs | `mkdir -Force a\b\c` | `mkdir -p a/b/c` |
| Copy | `Copy-Item src dest` | `cp src dest` |
| Copy dir | `Copy-Item src dest -Recurse` | `cp -r src dest` |
| Move/Rename | `Move-Item old new` | `mv old new` |
| Delete | `Remove-Item file` | `rm file` |
| Delete dir | `Remove-Item -Recurse dir` | `rm -r dir` |

## Reading Files

| Task | PowerShell | Bash |
|------|------------|------|
| Read file | `Get-Content file` | `cat file` |
| First N lines | `Get-Content file -Head N` | `head -n N file` |
| Last N lines | `Get-Content file -Tail N` | `tail -n N file` |
| Watch live | `Get-Content file -Wait` | `tail -f file` |
| Count lines | `(Get-Content file).Count` | `wc -l file` |

## Search

| Task | PowerShell | Bash |
|------|------------|------|
| Find text | `Select-String "p" file` | `grep "p" file` |
| Search recursive | `Get-ChildItem -Recurse \| Select-String "p"` | `grep -r "p" .` |
| Find file | `Get-ChildItem -Recurse -Filter "*.py"` | `find . -name "*.py"` |
| Fast search | | `rg "pattern"` |
| Fast find | | `fd "*.py"` |

## Text Processing

| Task | PowerShell | Bash |
|------|------------|------|
| Sort | `Sort-Object` | `sort` |
| Unique | `Unique` | `sort \| uniq` |
| Count | `Group-Object \| Sort Count` | `sort \| uniq -c \| sort -rn` |
| Cut column | `ForEach-Object { $_.Split(',')[0] }` | `cut -d',' -f1` |
| Replace | `-replace 'old','new'` | `sed 's/old/new/g'` |
| Print column | | `awk '{print $1}'` |

## Pipes & Redirection

| Op | PowerShell | Bash | Meaning |
|----|------------|------|---------|
| `\|` | `\|` | `\|` | Pipe output |
| `>` | `>` | `>` | Write to file |
| `>>` | `>>` | `>>` | Append to file |
| `<` | `<` | `<` | Read from file |
| Discard | `> $null` | `> /dev/null` | Throw away |
| Tee | `Tee-Object f` | `tee f` | Show + save |

## Processes

| Task | PowerShell | Bash |
|------|------------|------|
| List | `Get-Process` | `ps aux` |
| Kill PID | `Stop-Process -Id P` | `kill P` |
| Kill name | `Stop-Process -Name n` | `killall n` |
| Force | `Stop-Process -Id P -Force` | `kill -9 P` |
| Top | `Get-Process \| Sort CPU -Desc` | `top` / `htop` |
| Background | `Start-Job { s }` | `cmd &` |
| Jobs | `Get-Job` | `jobs` |

## Networking

| Task | PowerShell | Bash |
|------|------------|------|
| Ping | `Test-Connection h` | `ping h` |
| HTTP GET | `Invoke-WebRequest u` | `curl u` |
| Download | `Invoke-WebRequest -OutFile f u` | `curl -O u` |
| Port check | `Test-NetConnection h -Port P` | `nc -zv h P` |
| DNS | `Resolve-DnsName h` | `nslookup h` |
| IP | `Get-NetIPAddress` | `ip addr` |

## SSH

| Task | Command |
|------|---------|
| Connect | `ssh user@host` |
| Gen key | `ssh-keygen -t ed25519` |
| Copy key | `ssh-copy-id user@host` |
| SCP upload | `scp file user@host:/path/` |
| SCP download | `scp user@host:/path/file .` |

## Environment Variables

| Task | PowerShell | Bash |
|------|------------|------|
| Read | `$env:VAR` | `echo $VAR` |
| Set | `$env:VAR = "v"` | `export VAR="v"` |
| List all | `Get-ChildItem Env:` | `env` |
| Add PATH | `$env:PATH += ";new"` | `export PATH="$PATH:new"` |

## Keyboard Shortcuts

| Shortcut | Bash | Description |
|----------|------|-------------|
| Tab | Tab | Auto-complete |
| Ctrl+C | Ctrl+C | Cancel |
| Ctrl+Z | Ctrl+Z | Suspend |
| Ctrl+R | Ctrl+R | Search history |
| Ctrl+A | Ctrl+A | Start of line |
| Ctrl+E | Ctrl+E | End of line |
| Ctrl+L | Ctrl+L | Clear screen |
| Up | Up | Previous command |
| Down | Down | Next command |

---

> **Full Terminal section:** [Terminal](../02-terminal/README.md) | **Next:** [Git Quick Reference](git-quick-reference.md)
