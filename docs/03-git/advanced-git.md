# Advanced Git

> Stashing, bisecting, cherry-picking, submodules, and other powerful Git techniques.

> **Related:** [Collaboration](collaboration.md) | [Undoing Changes](undoing-changes.md)

---

## Git Stash

Save uncommitted changes temporarily and restore them later. Useful when you need to switch branches mid-task.

```bash
git stash                    # stash tracked changes
git stash push -m "wip: auth refactor"   # stash with message
git stash -u                 # include untracked files
git stash -a                 # include all files (including ignored)
```

```bash
git stash list               # show all stashes
git stash pop                # restore and remove latest stash
git stash apply stash@{2}    # restore a specific stash (keep it)
git stash drop stash@{0}     # delete a stash
git stash clear              # delete all stashes
```

## Cherry-Pick

Apply a specific commit from one branch to another without merging the whole branch:

```bash
git cherry-pick abc1234              # apply a specific commit
git cherry-pick abc1234..def5678     # apply a range of commits
git cherry-pick --no-commit abc1234  # apply changes without committing
```

## Git Bisect

Binary search through history to find which commit introduced a bug:

```bash
git bisect start
git bisect bad                 # current commit is broken
git bisect good v1.0           # v1.0 was working (tag or commit)
```

Git checks out the midpoint. Test it, then mark:

```bash
git bisect good                # this commit is clean
git bisect bad                 # this commit is broken
```

Repeat until Git identifies the first bad commit. Then:

```bash
git bisect reset               # return to original state
```

Automate with a script:

```bash
git bisect run pytest          # let Git run tests automatically
```

## Interactive Rebase

Edit, reorder, squash, or drop commits before merging:

```bash
git rebase -i HEAD~5           # rebase the last 5 commits interactively
```

An editor opens with a list of commands:

```
pick abc1234 Add login page
pick def5678 Fix typo in login
squash 789ghi Add tests for login
pick 012jkl Update README
```

| Command | Effect |
|---------|--------|
| `pick` | Keep the commit as-is |
| `reword` | Change the commit message |
| `squash` | Combine with the previous commit |
| `fixup` | Squash but discard the message |
| `edit` | Pause to amend the commit |
| `drop` | Remove the commit |

## Submodules

Include one Git repository inside another:

```bash
git submodule add https://github.com/user/lib.git lib/
git submodule init            # initialize submodules after clone
git submodule update          # fetch latest for all submodules
git clone --recursive url     # clone with submodules
```

Submodules pin a specific commit. Update them explicitly:

```bash
cd lib && git pull origin main
cd .. && git add lib && git commit -m "Update lib submodule"
```

## Worktrees

Check out multiple branches at the same time in different directories:

```bash
git worktree add ../project-hotfix hotfix
git worktree list
git worktree remove ../project-hotfix
```

## Patch Mode

Stage parts of a file instead of the whole thing:

```bash
git add -p                  # interactively stage hunks
```

Git shows each change hunk and prompts: `Stage this hunk? [y,n,q,a,d,s,e,?]`. Use this for clean, focused commits.

## Filter-Branch (Legacy) / Filter-Repo

Rewrite history to remove sensitive data or large files. Prefer `git-filter-repo`:

```bash
pip install git-filter-repo
git filter-repo --path .env --invert-paths
```

## Summary

| Technique | Command |
|-----------|---------|
| Save work temporarily | `git stash` |
| Apply a single commit | `git cherry-pick hash` |
| Find a bug's origin | `git bisect` |
| Rewrite commit history | `git rebase -i HEAD~n` |
| Embed another repo | `git submodule add url` |
| Check out multiple branches | `git worktree add path branch` |
| Stage specific hunks | `git add -p` |
