# Git Troubleshooting

> Common Git errors and how to fix them.

> **Related:** [Undoing Changes](undoing-changes.md) | [Collaboration](collaboration.md)

---

## What Is This?

Git errors can be cryptic. This page maps the most common error messages to their root cause and solution.

## Merge Conflicts

### "Automatic merge failed; fix conflicts and then commit the result"

| Problem | Cause | Solution |
|---------|-------|----------|
| Merge conflict in file.txt | Two branches changed the same lines | Open the file, look for `<<<<<<<`, `=======`, `>>>>>>>` markers, edit to the correct version, stage, and commit |
| Conflict markers left in file | Merge was aborted or forgotten | Find and remove markers from the file |

## Push Rejected

### "Updates were rejected because the remote contains work that you do not have locally"

| Problem | Cause | Solution |
|---------|-------|----------|
| Push rejected | Remote has commits you don't have locally | `git pull --rebase` or `git pull` to integrate remote changes, then push again |
| Force push needed (with caution) | You need to overwrite remote history | `git push --force-with-lease` (safer) or `git push --force` (use `--force-with-lease` instead) |

### "failed to push some refs"

| Problem | Cause | Solution |
|---------|-------|----------|
| Remote branch is protected | Branch rules prevent direct push | Open a Pull Request instead, or use `git push origin HEAD:branch-name` |

## Detached HEAD

### "You are in 'detached HEAD' state"

| Problem | Cause | Solution |
|---------|-------|----------|
| HEAD points directly to a commit, not a branch | You checked out a specific commit or tag | Create a branch: `git switch -c new-branch` |
| You made changes in detached HEAD and they'll be lost | Commits aren't attached to any branch | Create a branch to save them: `git switch -c save-my-work` |

## Accidental Hard Reset

### "I ran git reset --hard and lost my changes"

| Problem | Cause | Solution |
|---------|-------|----------|
| Commits are gone from branch history | `git reset --hard` removed them | Check the reflog: `git reflog`, then `git reset --hard HEAD@{n}` to go back |
| Uncommitted work is gone | `git reset --hard` discarded working tree changes | Recover from stash or editor history. Uncommitted changes are truly lost |

## Wrong Branch

### "I committed to main instead of a feature branch"

| Problem | Cause | Solution |
|---------|-------|----------|
| Commit is on the wrong branch | You forgot to switch branches first | `git switch -c feature-branch` (creates a branch at current position), then `git switch main` and `git reset --hard HEAD~1` |

## Authentication

### "Permission denied (publickey)"

| Problem | Cause | Solution |
|---------|-------|----------|
| SSH key not configured | Git can't authenticate | Check `ssh -T git@github.com`. Generate/add key: `ssh-keygen` then add to GitHub |
| Wrong remote URL | Using HTTPS when SSH is needed | `git remote set-url origin git@github.com:user/repo.git` |

### "Authentication failed"

| Problem | Cause | Solution |
|---------|-------|----------|
| Password or token expired | Credential manager is stale | Update credentials. Use `gh auth login` or generate a personal access token |

## File Tracking Issues

### "The file is in .gitignore but still tracked"

| Problem | Cause | Solution |
|---------|-------|----------|
| File was tracked before being ignored | Git continues tracking files already in the index | `git rm --cached file.txt` to stop tracking (keeps the file on disk), then commit |

### "Untracked files are shown even though they're in .gitignore"

| Problem | Cause | Solution |
|---------|-------|----------|
| The file was previously staged | Git caches the index | `git rm --cached -r .` and re-add. Check `.gitignore` spelling and path patterns |

## Repository Corruption

### "Object not found" or "fatal: bad object"

| Problem | Cause | Solution |
|---------|-------|----------|
| Git database is corrupted | Hardware failure, interrupted write, or manual editing of `.git/` | Try `git fsck` to diagnose. Restore from a fresh clone if needed |

## General Diagnostics

| Command | What It Tells You |
|---------|-------------------|
| `git status` | Current state: staged, unstaged, untracked files |
| `git log --oneline --graph` | Branch topology and commit history |
| `git diff` | What changed (unstaged) |
| `git reflog` | Every action you've taken recently |
| `git fsck` | Check repository integrity |
