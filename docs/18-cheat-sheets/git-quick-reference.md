# Git Quick Reference

> One-page command reference for Git. Print this or bookmark it.

---

## Setup

| Task | Command |
|------|---------|
| Set name | `git config --global user.name "Name"` |
| Set email | `git config --global user.email "email"` |
| Default branch | `git config --global init.defaultBranch main` |
| Editor | `git config --global core.editor "code --wait"` |
| aliases | `git config --global alias.co checkout` |

## Creating Repos

| Task | Command |
|------|---------|
| Init new repo | `git init` |
| Clone remote | `git clone url` |
| Clone to dir | `git clone url dir` |
| Shallow clone | `git clone --depth 1 url` |

## Staging & Committing

| Task | Command |
|------|---------|
| Status | `git status` |
| Stage file | `git add file` |
| Stage all | `git add .` |
| Stage chunks | `git add -p` |
| Unstage file | `git restore --staged file` |
| Commit | `git commit -m "message"` |
| Amend commit | `git commit --amend` |
| Skip staging | `git commit -am "message"` |

## Branching

| Task | Command |
|------|---------|
| List branches | `git branch` |
| List all | `git branch -a` |
| Create branch | `git branch name` |
| Switch branch | `git switch name` |
| Create + switch | `git switch -c name` |
| Delete branch | `git branch -d name` |
| Force delete | `git branch -D name` |
| Rename | `git branch -m old new` |

## Merging & Rebasing

| Task | Command |
|------|---------|
| Merge branch | `git merge branch` |
| Merge (no ff) | `git merge --no-ff branch` |
| Rebase current | `git rebase branch` |
| Interactive rebase | `git rebase -i HEAD~N` |
| Abort rebase | `git rebase --abort` |
| Continue rebase | `git rebase --continue` |
| Cherry-pick | `git cherry-pick commit` |

## Remote

| Task | Command |
|------|---------|
| List remotes | `git remote -v` |
| Add remote | `git remote add name url` |
| Remove remote | `git remote remove name` |
| Fetch | `git fetch` |
| Pull | `git pull` |
| Pull rebase | `git pull --rebase` |
| Push | `git push` |
| Push set-upstream | `git push -u origin branch` |
| Force push | `git push --force-with-lease` |

## Undoing Changes

| Task | Command |
|------|---------|
| Undo working dir | `git restore file` |
| Undo last commit | `git reset HEAD~1` |
| Undo (keep changes) | `git reset --soft HEAD~1` |
| Undo (discard) | `git reset --hard HEAD~1` |
| Revert commit | `git revert commit` |
| Stash changes | `git stash` |
| Stash + message | `git stash push -m "msg"` |
| List stashes | `git stash list` |
| Apply stash | `git stash apply` |
| Pop stash | `git stash pop` |
| Drop stash | `git stash drop` |

## Inspection

| Task | Command |
|------|---------|
| Log (one-line) | `git log --oneline` |
| Log (graph) | `git log --oneline --graph --all` |
| Log (diff) | `git log -p` |
| Show commit | `git show commit` |
| Diff (working) | `git diff` |
| Diff (staged) | `git diff --staged` |
| Diff branches | `git diff branch1..branch2` |
| Blame | `git blame file` |
| Search log | `git log --grep "text"` |
| Search changes | `git log -S "text"` |

## Tags

| Task | Command |
|------|---------|
| List tags | `git tag` |
| Create tag | `git tag v1.0` |
| Annotated tag | `git tag -a v1.0 -m "msg"` |
| Push tag | `git push origin v1.0` |
| Push all tags | `git push --tags` |

## Gitignore

| Pattern | Meaning |
|---------|---------|
| `*.log` | All .log files |
| `dir/` | Directory named dir |
| `!keep.log` | Negation (keep this) |
| `/TODO` | Root only |
| `doc/**/*.pdf` | Any .pdf in doc tree |

---

> **Full section:** [Git](../03-git/README.md) | **Next:** [GitHub](github-quick-reference.md)
