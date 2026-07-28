# Undoing Changes

> Git gives you multiple ways to undo at every stage of the workflow — from unmodifying a file to rewriting history.

> **Related:** [Basic Workflow](basic-workflow.md) | [Collaboration](collaboration.md)

---

## What Is It?

Mistakes are inevitable. Git provides tools to undo changes at every level: uncommitted changes, staged changes, committed changes, and even published history. The right tool depends on where the change is in the workflow.

## The Three States

```
Working Tree  →  Staging Area  →  Repository (committed)
     ↓                 ↓                  ↓
 git restore      git restore        git revert /
                  --staged           git reset
```

## Undoing Unstaged Changes

Discard changes in your working tree before they're staged:

```bash
git restore file.txt            # discard changes in one file
git restore .                   # discard all unstaged changes
git checkout -- file.txt        # older syntax
```

## Undoing Staged Changes

Unstage a file without losing its changes:

```bash
git restore --staged file.txt   # unstage but keep changes
git restore --staged .          # unstage everything
git reset HEAD file.txt         # older syntax (same effect)
```

To unstage AND discard changes:

```bash
git restore --staged --worktree file.txt
```

## Undoing Committed Changes

### Amend the Last Commit

If you forgot to include a file or made a typo in the message:

```bash
git commit --amend              # edit the commit message
git commit --amend --no-edit    # keep the message, add staged changes
```

**Never amend commits that have been pushed to a shared branch.**

### Revert (Safe for Shared History)

`git revert` creates a **new commit** that undoes a previous commit. It's safe because it doesn't rewrite history:

```bash
git revert HEAD                 # undo the most recent commit
git revert abc1234              # undo a specific commit by hash
```

### Reset (Local History Only)

`git reset` moves the branch pointer backward, discarding commits:

```bash
git reset --soft HEAD~1         # undo commit, keep changes staged
git reset --mixed HEAD~1        # undo commit, keep changes unstaged
git reset --hard HEAD~1         # undo commit, discard changes entirely
```

| Mode | Moves HEAD | Staging Area | Working Tree |
|------|-----------|--------------|--------------|
| `--soft` | Yes | Kept | Kept |
| `--mixed` (default) | Yes | Reset | Kept |
| `--hard` | Yes | Reset | Reset |

**Never use `--hard` if you're unsure what you'll lose.**

## The Reflog: Your Safety Net

Every action in Git is logged in the reflog. Even "lost" commits can be found:

```bash
git reflog                  # show the reflog
git checkout HEAD@{2}       # go back to where you were two moves ago
```

The reflog only tracks local activity — it's your last resort when things go wrong.

## Summary

| What you want | Command |
|---------------|---------|
| Discard unstaged changes | `git restore file` |
| Unstage a file | `git restore --staged file` |
| Fix last commit message | `git commit --amend` |
| Undo a commit (safe) | `git revert HEAD` |
| Remove commits (local) | `git reset --hard HEAD~n` |
| Recover lost commits | `git reflog` |
