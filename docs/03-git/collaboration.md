# Collaboration

> Git workflows for working with others: merging strategies, conflict resolution, and the fork & PR model.

> **Related:** [Branching & Merging](branching.md) | [Working with Remotes](remote-repos.md)

---

## What Is It?

Collaboration in Git revolves around sharing commits through remotes. Two key decisions shape every collaboration workflow: **how you integrate changes** (merge vs rebase) and **how you share access** (shared repo vs fork & PR).

## Merge vs Rebase

Both integrate changes from one branch into another, but they produce different histories.

### Merge

```bash
git checkout main
git merge feature-x
```

Creates a merge commit that preserves the exact history of both branches. The timeline shows when branches diverged and merged.

**Use when:** You want an accurate historical record of how development happened.

### Rebase

```bash
git checkout feature-x
git rebase main
```

Re-plays commits from `feature-x` on top of `main`, creating a linear history. Each commit is rewritten.

**Use when:** You want a clean, linear history before merging.

### Rebase Workflow

```bash
git switch feature-x
git rebase main
# resolve any conflicts, then:
git add fixed-file.txt
git rebase --continue
# or: git rebase --abort
git switch main
git merge feature-x    # fast-forward now
```

| Aspect | Merge | Rebase |
|--------|-------|--------|
| History | Preserves branch structure | Linear |
| Safety | Non-destructive | Rewrites commits |
| Conflict resolution | Once (in merge commit) | Per commit |
| When to use | Public/shared branches | Private/feature branches |

## Resolving Merge Conflicts

When Git can't automatically merge, you'll see:

```bash
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

Conflict markers appear in the file:

```
<<<<<<< HEAD
current branch's version
=======
incoming branch's version
>>>>>>> feature-x
```

### Steps to Resolve

1. Open the conflicted file
2. Decide which version to keep (or edit to a third option)
3. Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage the file: `git add file.txt`
5. Complete the merge: `git commit` (or `git rebase --continue`)

### Tools

```bash
git mergetool              # launch visual merge tool
git diff                   # see conflicting differences
git log --merge            # see commits that caused conflict
```

## Fork & Pull Request Workflow

Common in open-source and team environments where not everyone has write access:

1. Fork the upstream repo on GitHub
2. Clone your fork: `git clone https://github.com/you/repo.git`
3. Add upstream remote: `git remote add upstream https://github.com/original/repo.git`
4. Create a feature branch: `git switch -c my-feature`
5. Make changes and commit
6. Push to your fork: `git push origin my-feature`
7. Open a Pull Request on GitHub
8. When approved, merge and sync:

```bash
git switch main
git pull upstream main       # get latest from upstream
git push origin main         # sync your fork
```

## Keeping a Feature Branch Updated

```bash
git switch feature-x
git fetch upstream
git rebase upstream/main     # or: git merge upstream/main
```

Regularly syncing prevents painful conflicts later.

## Key Practices

- **Commit early, commit often** — small commits are easier to review and revert
- **Write descriptive commit messages** — your future self will thank you
- **Keep feature branches short-lived** — days, not weeks
- **Communicate before rebasing shared branches** — rebasing a pushed branch forces teammates to reset
- **Use `.gitignore`** — don't commit build artifacts, dependencies, or secrets
