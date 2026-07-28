# Git Internals

> How Git works under the hood: objects, refs, the Three Trees, and the data model that makes Git tick.

> **Related:** [What Is Git?](what-is-git.md) | [Undoing Changes](undoing-changes.md)

---

## What Is It?

Git is fundamentally a key-value store of **objects**. Understanding the object model demystifies Git's behavior and makes advanced operations intuitive.

## The Object Model

Git stores everything in four types of objects, each identified by a SHA-1 hash (40-character hex string):

| Object | What It Stores | Example |
|--------|---------------|---------|
| **Blob** | File contents | The text inside `main.py` |
| **Tree** | Directory listing | `main.py -> blob abc123`, `src/ -> tree def456` |
| **Commit** | Snapshot metadata | Author, message, parent commits, tree hash |
| **Tag** | A named reference | A human-readable name for a specific commit |

A commit points to a tree that represents the entire project at that point. If files haven't changed, they reuse the same blobs — Git doesn't duplicate data.

```
Commit abc123
  Author: Alice
  Message: "Add login"
  Parent: def456
  Tree: 789ghi

    Tree 789ghi (root)
      main.py    -> blob aaa111
      src/       -> tree bbb222
        utils.py -> blob ccc333
        auth.py  -> blob ddd444
```

## The Three Trees

Git tracks three trees at all times:

| Tree | What It Is | Command to Inspect |
|------|-----------|-------------------|
| **HEAD** | The last commit on the current branch | `git show HEAD` |
| **Index (Staging Area)** | The proposed next commit | `git ls-files --stage` |
| **Working Tree** | The actual files on disk | `git status` |

The basic workflow is moving files between these three trees:

```
Working Tree → Index → HEAD
  (edit)     (stage)  (commit)
```

## Refs and HEAD

A **ref** is a pointer to a commit. Branches, tags, and HEAD are all refs:

| Ref | What It Points To | Located At |
|-----|------------------|------------|
| `refs/heads/main` | The latest commit on main | `.git/refs/heads/main` |
| `refs/tags/v1.0` | A specific commit | `.git/refs/tags/v1.0` |
| `HEAD` | The current branch (not commit) | `.git/HEAD` |

HEAD is normally **attached** to a branch (e.g., `ref: refs/heads/main`). When you checkout a specific commit, HEAD becomes **detached**.

## The Reflog

Git records every movement of HEAD and branch tips in the reflog:

```bash
git reflog
```

This is your safety net. Even if you reset or rebase, the reflog keeps track of where you were — for 90 days by default.

## Plumbing Commands

Git's "plumbing" commands expose the internal model:

```bash
git hash-object file.txt         # compute object hash
git cat-file -p abc123           # view object contents
git ls-tree HEAD                 # list the tree at HEAD
git rev-parse HEAD               # show current commit hash
```

## Why This Matters

- **Git is not file-based** — it's snapshot-based. This is why moving between branches is fast.
- **Commits are cheap** — they're just pointers. Branch and commit freely.
- **The staging area exists** because Git separates the working tree and index. You can prepare a commit incrementally.
- **Rebasing rewrites commits** — because a commit includes its parent hash, changing parents creates entirely new objects.
