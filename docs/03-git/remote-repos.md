# Working with Remotes

> Remotes connect your local repository to hosted copies on GitHub, GitLab, or other servers for backup and collaboration.

> **Related:** [Branching & Merging](branching.md) | [Collaboration](collaboration.md)

---

## What Is It?

A remote is a version of your repository hosted on another machine — usually a service like GitHub. You push commits to share them and pull commits to incorporate others' work.

## Managing Remotes

### View Remotes

```bash
git remote            # list remote names
git remote -v         # list with URLs (fetch & push)
```

### Add a Remote

```bash
git remote add origin https://github.com/user/repo.git
```

By convention, `origin` is the name of your primary remote.

### Remove or Rename

```bash
git remote remove origin
git remote rename origin upstream
```

## The Core Remote Workflow

### Pushing

```bash
git push origin main          # push local main to origin's main
git push -u origin main       # set upstream tracking (-u), then push
git push --delete origin branch-name   # delete remote branch
```

The `-u` flag sets the upstream so future `git push` and `git pull` work without specifying the remote and branch.

### Pulling

```bash
git pull                      # fetch from upstream + merge (shortcut)
git pull origin main          # pull specific remote branch
```

`git pull` is shorthand for `git fetch` followed by `git merge`.

### Fetching

```bash
git fetch                     # download remote data without merging
git fetch origin              # fetch from origin
git fetch --prune             # remove stale remote-tracking references
```

Unlike `pull`, `fetch` doesn't touch your working tree — it just downloads new data. Use it when you want to inspect changes before integrating them.

## Remote-Tracking Branches

Remote-tracking branches (like `origin/main`) show where the remote's branches were the last time you fetched:

```bash
git branch -r                 # list remote-tracking branches
git log origin/main           # see remote's history without switching
git diff main origin/main     # see how your branch and remote differ
```

## Multiple Remotes

It's common to have multiple remotes, especially in open-source:

```bash
git remote add upstream https://github.com/original/repo.git
```

Then `origin` points to your fork and `upstream` points to the original repo.

| Task | Command |
|------|---------|
| List remotes | `git remote -v` |
| Add a remote | `git remote add name url` |
| Push to remote | `git push remote branch` |
| Pull from remote | `git pull remote branch` |
| Fetch from remote | `git fetch remote` |
| Delete remote branch | `git push remote --delete branch` |
