# Foundations Quick Reference

> One-page reference for file systems, paths, OS differences, and core dev tools. Print this or bookmark it.

---

## File Paths

| Concept | Windows | Mac/Linux |
|---------|---------|-----------|
| Separator | `\` | `/` |
| Absolute | `C:\Users\name\file` | `/home/name/file` |
| Relative | `..\sibling\file` | `../sibling/file` |
| Home | `%USERPROFILE%` or `~` | `$HOME` or `~` |
| Current dir | `.` | `.` |
| Parent dir | `..` | `..` |
| Root | `C:\` | `/` |

## File Extensions

| Extension | Type | Common Tools |
|-----------|------|--------------|
| `.js` | JavaScript | Node.js, Browsers |
| `.ts` | TypeScript | tsc, Node.js |
| `.py` | Python | Python |
| `.rs` | Rust | cargo |
| `.go` | Go | go build |
| `.java` | Java | javac, Maven, Gradle |
| `.c` / `.cpp` | C / C++ | gcc, clang |
| `.html` | HTML | Browsers |
| `.css` | CSS | Browsers |
| `.json` | JSON | Any text editor |
| `.yaml` / `.yml` | YAML | Any text editor |
| `.toml` | TOML | Any text editor |
| `.xml` | XML | Any text editor |
| `.md` | Markdown | Renderers, GitHub |
| `.sql` | SQL | Database clients |
| `.sh` | Shell script | Bash |
| `.ps1` | PowerShell script | PowerShell |
| `.dockerfile` | Docker config | Docker |
| `.env` | Environment vars | dotenv libraries |

## Hidden Files / Directories

| OS | Pattern | Example |
|----|---------|---------|
| Windows | Name starts with nothing, hidden attribute | `.git` (hidden by default in Explorer) |
| Mac/Linux | Name starts with `.` | `.git`, `.env`, `.bashrc` |
| Show hidden (Win) | File Explorer → View → Hidden items | — |
| Show hidden (Mac) | `defaults write com.apple.finder AppleShowAllFiles YES` | — |
| Show hidden (Linux) | `ls -la` | — |

## OS-Specific Commands

### System Info

| Task | Windows | Mac | Linux |
|------|---------|-----|-------|
| OS name | `systeminfo \| findstr /B "OS"` | `sw_vers` | `uname -a` |
| CPU info | `systeminfo \| findstr "Processor"` | `sysctl -n machdep.cpu.brand_string` | `lscpu` |
| Memory | `systeminfo \| findstr "Memory"` | `sysctl -n hw.memsize` | `free -h` |
| Disk usage | `Get-PSDrive C` | `df -h` | `df -h` |
| Running processes | `Get-Process` | `ps aux` | `ps aux` |
| Environment vars | `Get-ChildItem Env:` | `env` | `env` |

### Package Managers (System)

| OS | Package Manager | Install Example |
|----|-----------------|-----------------|
| Windows | winget / chocolatey / scoop | `winget install Git.Git` |
| Mac | Homebrew | `brew install git` |
| Linux (Debian) | apt | `sudo apt install git` |
| Linux (Fedora) | dnf | `sudo dnf install git` |
| Linux (Arch) | pacman | `sudo pacman -S git` |

## Git Ignore Patterns

| Pattern | Matches |
|---------|---------|
| `*.log` | All `.log` files anywhere |
| `*.log!debug.log` | All `.log` except `debug.log` |
| `/build` | `build` in root only |
| `build/` | `build` anywhere |
| `**/temp` | `temp` in any directory |
| `doc/**/*.pdf` | Any `.pdf` under `doc/` |
| `node_modules/` | `node_modules` anywhere |

## Common Config File Locations

| Tool | Config File | Location |
|------|-------------|----------|
| Git | `.gitconfig` | `~/.gitconfig` |
| npm | `.npmrc` | `~/.npmrc` |
| Python | `.flake8`, `pyproject.toml` | Project root |
| VS Code | `settings.json` | `.vscode/settings.json` |
| Neovim | `init.lua` | `~/.config/nvim/init.lua` |
| Docker | `Dockerfile` | Project root |
| ESLint | `.eslintrc.js` | Project root |
| Prettier | `.prettierrc` | Project root |

## Port Numbers

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 3000 | React/Next.js/Express dev |
| 5000 | Flask/ASP.NET |
| 5173 | Vite dev server |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 8080 | Alternative HTTP |
| 8000 | Django/Laravel |
| 27017 | MongoDB |
| 3306 | MySQL |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|---------|
| Mixing path separators | Breaks on other OS | Use `path.join()` or `os.path.join()` |
| Hardcoding paths | Fails on other machines | Use `~` or env vars |
| Editing `.git` manually | Corrupts repo | Use `git` commands only |
| Ignoring OS differences | "Works on my machine" | Test on target OS or use CI |
| Committing `.env` | Leaks secrets | Add to `.gitignore` |

---

> **Full section:** [Foundations](../01-foundations/README.md) | **Next:** [Terminal](terminal-quick-reference.md)
