# PowerShell

> PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration framework.

---

## What Is It?

PowerShell is a shell and scripting language made by Microsoft. Unlike traditional shells that deal in text, PowerShell deals in **objects**. This means commands return structured data you can filter, sort, and manipulate programmatically.

| Feature | PowerShell | Traditional Shell |
|---------|------------|-------------------|
| Input/Output | Objects (.NET) | Plain text |
| Naming | `Verb-Noun` (e.g., `Get-ChildItem`) | Short commands (e.g., `ls`) |
| Configuration | `Profile.ps1` | `.bashrc`, `.zshrc` |
| Platform | Windows, macOS, Linux | Mostly Linux/macOS |

## Why Does It Exist?

1. **Windows automation** - Automate Windows administration tasks
2. **Object pipeline** - Pass structured data between commands
3. **.NET integration** - Access the entire .NET framework
4. **Consistency** - Predictable `Verb-Noun` naming convention
5. **Remoting** - Manage remote Windows machines

## Mental Model

Think of PowerShell as a **factory assembly line**:

```mermaid
graph LR
    A[Get raw materials<br>Get-Process] --> B[Transform<br>Select-Object]
    B --> C[Package<br>Export-Csv]
    C --> D[Ship<br>Send to file/network]
```

Each command (cmdlet) produces objects, and the pipe `|` passes those objects to the next cmdlet. The next cmdlet doesn't need to parse text - it receives actual objects with properties and methods.

## When Should I Use It?

| Use PowerShell When | Use Something Else When |
|--------------------|-----------------------|
| Automating Windows tasks | Writing cross-platform scripts (use Bash) |
| Managing Active Directory | Working on Linux servers (use Bash) |
| Querying WMI/CIM | Simple one-line tasks (use cmd) |
| Working with .NET objects | Running on macOS (use Zsh) |
| Windows system administration | Docker/CI pipelines (use Bash) |
| Parsing structured data | Simple text manipulation (use cmd) |

## Cheat Sheet

### Essential Commands

| Task | Command | Description |
|------|---------|-------------|
| List files | `Get-ChildItem` or `ls` | List directory contents |
| Change dir | `Set-Location` or `cd` | Change current directory |
| Copy | `Copy-Item` or `cp` | Copy files/folders |
| Move | `Move-Item` or `mv` | Move/rename files |
| Delete | `Remove-Item` or `rm` | Delete files/folders |
| Create dir | `New-Item -ItemType Directory` | Create a folder |
| Read file | `Get-Content` or `cat` | Display file contents |
| Write file | `Set-Content` or `sc` | Write to a file |
| Find text | `Select-String` or `sls` | Search for patterns |
| See processes | `Get-Process` | List running processes |
| Stop process | `Stop-Process` | Kill a process |
| Environment var | `$env:VAR_NAME` | Read an env var |

### Command Syntax

```powershell
# Verb-Noun pattern
Get-Process                    # Get all processes
Get-Process -Name chrome       # Get specific process
Get-Process | Where-Object {$_.CPU -gt 100}  # Filter objects

# Aliases (shortcuts)
ls      # Get-ChildItem
cd      # Set-Location
cp      # Copy-Item
mv      # Move-Item
rm      # Remove-Item
cat     # Get-Content
echo    # Write-Output
```

### Common Parameters

| Parameter | Short | Description |
|-----------|-------|-------------|
| `-WhatIf` | `-wi` | Show what would happen without doing it |
| `-Confirm` | `-cf` | Ask before executing |
| `-Force` | `-fo` | Override restrictions |
| `-Verbose` | `-vb` | Show detailed output |
| `-ErrorAction` | `-ea` | How to handle errors |

## Step-by-Step Workflow

### 1. Check Your PowerShell Version

```powershell
$PSVersionTable.PSVersion
```

### 2. See Available Commands

```powershell
Get-Command                    # All commands
Get-Command -Verb Get          # Commands that "Get" things
Get-Help Get-Process -Full     # Detailed help for a command
```

### 3. Explore Objects

```powershell
Get-Process | Get-Member       # See properties and methods
Get-Process | Select-Object Name, CPU, Id | Sort-Object CPU -Descending
```

### 4. Create a Simple Script

```powershell
# save as script.ps1
$files = Get-ChildItem -Path "." -Recurse -File
$files | Group-Object Extension | Sort-Object Count -Descending | Select-Object Count, Name
```

### 5. Run the Script

```powershell
.\script.ps1
```

## Real Project Examples

### Organize Downloads Folder

```powershell
Get-ChildItem "$env:USERPROFILE\Downloads" -File | ForEach-Object {
    $ext = $_.Extension.TrimStart('.')
    $dest = "$env:USERPROFILE\Downloads\$ext"
    if (-not (Test-Path $dest)) { New-Item -ItemType Directory -Path $dest -Force }
    Move-Item $_.FullName -Destination $dest
}
```

### Find Large Files

```powershell
Get-ChildItem -Path "C:\" -Recurse -File -ErrorAction SilentlyContinue |
    Where-Object { $_.Length -gt 100MB } |
    Sort-Object Length -Descending |
    Select-Object @{N="SizeMB"; E={[math]::Round($_.Length/1MB)}}, FullName
```

### Batch Rename Files

```powershell
Get-ChildItem "*.txt" | Rename-Item -NewName { $_.Name -replace 'old', 'new' }
```

### Check Disk Space

```powershell
Get-PSDrive -PSProvider FileSystem | Select-Object Name, @{N="UsedGB"; E={[math]::Round($_.Used/1GB,2)}}, @{N="FreeGB"; E={[math]::Round($_.Free/1GB,2)}}
```

## Best Practices

- **Use `Verb-Noun` names** - Don't use aliases in scripts; they're harder to read
- **Always use `-ErrorAction`** - Handle errors explicitly in scripts
- **Use `-WhatIf` first** - Test destructive operations before running them
- **Quote file paths** - Always quote paths that might contain spaces
- **Use `$PSScriptRoot`** - Reference files relative to your script's location
- **Set execution policy** - `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`

## Common Mistakes

> **Warning:** PowerShell scripts use `.ps1` extension. Right-click > "Run with PowerShell" to execute them. Don't double-click - it will just open in Notepad.

| Mistake | Problem | Solution |
|---------|---------|----------|
| Using aliases in scripts | Hard to read, break on different systems | Use full cmdlet names |
| Not quoting paths | Breaks on spaces in paths | Always wrap in `"quotes"` |
| Forgetting `-Recurse` | Only operates on top level | Add `-Recurse` for nested folders |
| Running as admin when not needed | Security risk | Only elevate when required |
| Using `Write-Host` | Output can't be piped | Use `Write-Output` or just output the object |

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| "UnauthorizedAccess" | Execution policy | Run `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| "Command not found" | Command doesn't exist | Run `Get-Command` to see available commands |
| Script won't run | File path issue | Use `.\script.ps1` with `.\` prefix |
| Output is ugly | Formatting issue | Pipe to `Format-Table` or `Format-List` |
| Slow performance | Large dataset | Use `-Filter` parameter instead of `Where-Object` |

## Related Topics

- [Bash](bash.md) - Unix/Linux shell comparison
- [PowerShell vs Bash](powershell-vs-bash.md) - Side-by-side comparison
- [Environment Variables](environment-variables.md) - PowerShell env vars
- [Pipes and Redirection](pipes-and-redirection.md) - PowerShell pipeline
- [What Is a Terminal?](what-is-a-terminal.md) - Terminal fundamentals

## Further Learning

- [PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/) - Official docs
- [PowerShell in a Nutshell](https://www.oreilly.com/library/view/powershell-in-a/9781492080640/) - Comprehensive reference
- [r/PowerShell](https://reddit.com/r/PowerShell) - Community help
- [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) - Linting for PowerShell scripts

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
