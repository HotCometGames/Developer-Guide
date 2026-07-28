# Git Configuration

> Setting up Git, ignoring files, and configuring hooks and attributes.

> **Related:** [Basic Workflow](basic-workflow.md) | [Troubleshooting](git-troubleshooting.md)

---

## What Is It?

Git's behavior is controlled through configuration files, `.gitignore` patterns, `.gitattributes` settings, and hooks that run scripts at key lifecycle events.

## Git Config

Configuration lives at three levels:

| Level | File | Scope |
|-------|------|-------|
| `--system` | `[install]/etc/gitconfig` | All users on the machine |
| `--global` | `~/.gitconfig` or `~/.config/git/config` | Your user account |
| `--local` | `.git/config` | Current repository (default) |

### Essential Settings

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
```

### Aliases

Shorten common commands:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"
```

After setting aliases, `git st` runs `git status` and `git lg` shows a compact graph.

### Viewing Config

```bash
git config --list            # all config (all levels)
git config --global --list   # global config only
git config user.name         # single value
```

## .gitignore

A `.gitignore` file tells Git which files to ignore. Place it in the repository root or in subdirectories.

### Common Patterns

```gitignore
# Dependencies
node_modules/
vendor/
packages/

# Build output
dist/
build/
*.exe
*.dll

# Environment
.env
.env.local
*.env

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Logs
*.log
```

### Global .gitignore

For patterns you want to ignore across all repos:

```bash
git config --global core.excludesFile ~/.gitignore_global
```

## .gitattributes

Configure how Git handles file-specific behavior:

```gitignore
# Normalize line endings
* text=auto

# Declare binary files
*.png binary
*.jpg binary

# Specify line endings
*.sh text eol=lf
*.bat text eol=crlf
*.md text
```

## Git Hooks

Hooks are scripts in `.git/hooks/` that run automatically at specific points. The `pre-commit` framework makes them easy to manage:

```bash
pip install pre-commit
pre-commit install
```

Example `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
```

### Common Git Hooks

| Hook | Trigger | Common Use |
|------|---------|-----------|
| `pre-commit` | Before each commit | Lint, format, check secrets |
| `pre-push` | Before pushing | Run tests, check builds |
| `commit-msg` | After commit message is written | Validate message format |
| `post-merge` | After a merge completes | Update dependencies |

Hooks are local and not committed by default. Use `pre-commit` or a hooks directory shared via `core.hooksPath`.

## SSH Keys

Configure Git to use SSH instead of HTTPS for push access:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
# Add public key to GitHub/GitLab
git remote set-url origin git@github.com:user/repo.git
```

## GPG Signing

Sign commits to verify your identity:

```bash
git config --global commit.gpgSign true
git config --global user.signingkey KEY_ID
```

## Summary

| Task | Command |
|------|---------|
| Set user name | `git config --global user.name "Name"` |
| Set editor | `git config --global core.editor "code --wait"` |
| Create alias | `git config --global alias.co checkout` |
| View config | `git config --list` |
| Create .gitignore | Add patterns to `.gitignore` |
| Install hooks | `pre-commit install` |
| Set SSH remote | `git remote set-url origin git@github.com:user/repo.git` |
