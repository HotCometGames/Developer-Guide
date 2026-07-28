# Basic Workflow

> The core Git cycle: init, stage, commit, and inspect your history.

> **Related:** [What Is Git?](what-is-git.md) | [Branching & Merging](branching.md)

---

## What Is It?

The basic Git workflow is a loop: make changes to files, stage the ones you want to keep, commit them with a message, and repeat. This page covers the commands you'll use 90% of the time.

## Setting Up a Repository

### Starting from Scratch

```bash
git init
```

Turns the current directory into a Git repository. A hidden `.git/` folder is created to store all version data.

### Cloning an Existing Repository

```bash
git clone https://github.com/user/repo.git
```

Copies an existing remote repository to your machine, complete with all history.

## The Daily Workflow

### 1. Check the Status

```bash
git status
```

Shows which files are modified, staged, or untracked. Run this constantly.

### 2. Stage Changes

```bash
git add file.txt          # stage a specific file
git add .                 # stage all changes in the directory
git add -p                # stage interactively (patch mode)
```

Staging tells Git which changes you want to include in the next commit.

### 3. Commit

```bash
git commit -m "Add user login feature"
```

Takes a snapshot of everything in the staging area. Write clear, concise commit messages:

| Message | Quality |
|---------|---------|
| "Fix bug" | Bad — too vague |
| "Fix crash when user submits empty form" | Good |
| "Add tests for login validation" | Good |
| "wip" | Bad — what changed? |

### 4. View History

```bash
git log                 # full history
git log --oneline       # compact one-line view
git log --graph         # show branch topology
```

### 5. See What Changed

```bash
git diff                # unstaged changes
git diff --staged       # staged changes (what will be committed)
```

## Undoing Before Commit

```bash
git restore file.txt      # discard unstaged changes in a file
git restore --staged file.txt   # unstage a file (keep changes)
```

## Ignoring Files

Create a `.gitignore` file in the root of your repository:

```gitignore
node_modules/
.env
*.log
```

Git will never track files matching these patterns.

## Summary

| Step | Command |
|------|---------|
| Start a repo | `git init` |
| Clone a repo | `git clone url` |
| Check status | `git status` |
| Stage changes | `git add file` |
| Commit | `git commit -m "message"` |
| View history | `git log --oneline` |
| See changes | `git diff` |
| Discard changes | `git restore file` |
