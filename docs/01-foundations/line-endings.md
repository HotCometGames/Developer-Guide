# Line Endings

> The invisible difference between how Windows and Unix systems mark the end of a line — and how to stop it from causing chaos.

> **Related:** [Character Encoding](character-encoding.md) | [Operating Systems](operating-systems.md)

---

## What Is It?

Line endings are the **character(s) that mark the end of a line of text** in a file.

| Style | Characters | Bytes | Used By |
|-------|-----------|-------|---------|
| LF (Line Feed) | `\n` | `0x0A` | Linux, macOS, modern tools |
| CRLF (Carriage Return + Line Feed) | `\r\n` | `0x0D 0x0A` | Windows |
| CR (Carriage Return) | `\r` | `0x0D` | Classic macOS (pre-OS X) — obsolete |

## Why Does It Exist?

This is a historical accident from the era of teletype printers:

- **LF** — moves the paper up one line
- **CR** — moves the carriage back to the left margin

Unix adopted LF alone. Windows kept both. This split has caused endless frustration ever since.

## Mental Model

### What You See vs What's Stored

```text
You see:                Stored as LF:          Stored as CRLF:
line one                line one\n             line one\r\n
line two                line two\n             line two\r\n
line three              line three\n           line three\r\n
```

In most editors, both look identical. The difference is invisible until you:

- Open a file in a different tool
- See `^M` characters at the end of lines (`cat` on Unix shows CRLF as `^M`)
- Run a linter or formatter that complains
- See an entire file as changed in git when only line endings differ

### The Git Dimension

Git can automatically convert line endings:

```text
Git setting:        What happens:
core.autocrlf=true  Checkout CRLF, commit LF  (Windows — recommended)
core.autocrlf=input  Keep as-is, commit LF      (Mac/Linux — recommended)
core.autocrlf=false  No conversion               (keep whatever is on disk)
```

**Why this matters:** Without proper settings, a single `git add` can show every line of every file as changed, making code review impossible.

### Per-Language Conventions

| Language / Tool | Convention | Why |
|----------------|-----------|-----|
| Python | LF | PEP 8, Unix standard |
| JavaScript / TypeScript | LF | ESLint, Prettier default |
| C# | CRLF | Visual Studio tradition |
| Makefiles | LF | Make requires LF (CRLF breaks Make) |
| Shell scripts | LF | Shebang requires LF |
| PowerShell scripts | Either | Both work (but LF preferred for cross-platform) |

## Cheat Sheet

```
# Git — Recommended setup
Windows:   git config --global core.autocrlf true
Mac/Linux: git config --global core.autocrlf input

# Normalize a file
LF → CRLF:  unix2dos file.txt
CRLF → LF:  dos2unix file.txt

# Git: normalize entire repo
git add --renormalize .

# Detect line endings
Linux/Mac:  file filename
Windows:    In VS Code, bottom-right corner shows "CRLF" or "LF"

# VS Code setting
"files.eol": "\n"    # Always LF
"files.eol": "\r\n"  # Always CRLF
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Ignoring line ending settings | First commit shows every file as changed | Set `core.autocrlf` before cloning |
| Mixed endings in one file | Linters fail, tools produce weird output | Normalize with `dos2unix` or editor |
| Committing shell scripts with CRLF | `./script.sh: command not found` or bad interpreter | Use LF for shell scripts |
| Not adding `.gitattributes` | Settings don't apply to teammates | Create a `.gitattributes` file in the repo |
| Thinking it doesn't matter | Wastes hours on invisible bugs | Fix it once, set it correctly, move on |

### Recommended `.gitattributes`

```text
# Auto-detect and normalize
* text=auto

# Explicit overrides
*.sh    text eol=lf
*.bash  text eol=lf
*.ps1   text eol=crlf
*.bat   text eol=crlf
*.sln   text eol=crlf
*.csproj text eol=crlf
*.md    text eol=lf
*.json  text eol=lf
```

## Related Topics

- [Character Encoding](character-encoding.md) — Another invisible text format issue
- [Operating Systems](operating-systems.md) — Why Windows and Unix handle this differently
- [The File System](the-file-system.md) — How text files are stored on disk

## Further Learning

- [Mind the End of Your Line](https://adaptivepatchwork.com/2012/03/01/mind-the-end-of-your-line/) — Git line ending best practices
- [git-config docs](https://git-scm.com/docs/git-config#Documentation/git-config.txt-coreautocrlf) — Official Git documentation
- [What is the difference between `\r` and `\n`?](https://stackoverflow.com/questions/1279779) — Stack Overflow

---

> **Next:** [Binary and Hex](binary-and-hex.md) | **Previous:** [Character Encoding](character-encoding.md)
