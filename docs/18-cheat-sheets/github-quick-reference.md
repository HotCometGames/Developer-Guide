# GitHub Quick Reference

> One-page reference for GitHub and the `gh` CLI. Print this or bookmark it.

---

## GitHub CLI (`gh`) Setup

| Task | Command |
|------|---------|
| Login | `gh auth login` |
| Status | `gh auth status` |
| Set editor | `gh config set editor "code --wait"` |
| Default browser | `gh config set browser "edge"` |

## Repositories

| Task | Command |
|------|---------|
| Create repo | `gh repo create name --public` |
| Create private | `gh repo create name --private` |
| Clone | `gh repo clone owner/repo` |
| Fork | `gh repo fork owner/repo` |
| List my repos | `gh repo list` |
| View in browser | `gh repo view --web` |
| Set default | `gh repo set-default owner/repo` |

## Pull Requests

| Task | Command |
|------|---------|
| Create PR | `gh pr create` |
| Create (filled) | `gh pr create -t "title" -b "body"` |
| List PRs | `gh pr list` |
| View PR | `gh pr view 123` |
| Checkout PR | `gh pr checkout 123` |
| Diff PR | `gh pr diff 123` |
| Merge PR | `gh pr merge 123` |
| Merge (squash) | `gh pr merge 123 --squash` |
| Close PR | `gh pr close 123` |
| Review PR | `gh pr review 123 --approve` |
| Comment | `gh pr comment 123 -b "body"` |
| Checks | `gh pr checks 123` |

## Issues

| Task | Command |
|------|---------|
| Create issue | `gh issue create` |
| Create (filled) | `gh issue create -t "title" -b "body"` |
| List issues | `gh issue list` |
| View issue | `gh issue view 123` |
| Close issue | `gh issue close 123` |
| Reopen | `gh issue reopen 123` |
| Comment | `gh issue comment 123 -b "body"` |
| Transfer | `gh issue transfer 123 repo` |

## Actions (CI/CD)

| Task | Command |
|------|---------|
| List workflows | `gh workflow list` |
| List runs | `gh run list` |
| View run | `gh run view 123` |
| Watch run | `gh run watch 123` |
| Rerun failed | `gh run rerun 123 --failed` |
| Trigger workflow | `gh workflow run name` |
| View logs | `gh run view 123 --log` |

## Releases

| Task | Command |
|------|---------|
| List releases | `gh release list` |
| Create release | `gh release create v1.0` |
| With notes | `gh release create v1.0 -n "notes"` |
| Download asset | `gh release download v1.0` |
| View release | `gh release view v1.0` |

## Gists

| Task | Command |
|------|---------|
| Create gist | `gh gist create file` |
| List gists | `gh gist list` |
| View gist | `gh gist view id` |
| Edit gist | `gh gist edit id` |

## Secrets & Variables

| Task | Command |
|------|---------|
| Set secret | `gh secret set NAME` |
| Set (from file) | `gh secret set NAME < file` |
| List secrets | `gh secret list` |
| Delete secret | `gh secret delete NAME` |
| Set variable | `gh variable set NAME -b "value"` |
| List variables | `gh variable list` |

## Common Workflows

### Create feature branch + PR

```bash
git checkout -b feature/my-thing
# ... work ...
git push -u origin feature/my-thing
gh pr create -t "Add my thing" -b "Description"
```

### Review a PR locally

```bash
gh pr checkout 42
# test changes
gh pr review 42 --approve -b "LGTM"
gh pr merge 42 --squash
```

### Debug a failing CI run

```bash
gh run list
gh run view 123 --log
gh run rerun 123 --failed
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Force push to main | Overwrites others' work | Use `--force-with-lease` |
| Commit secrets | Leaks credentials | Use `.gitignore` + `gh secret set` |
| PR with no description | Reviewers lack context | Use `gh pr create -b` with template |
| Merge without review | Code quality drops | Require reviews in repo settings |

## Quick Tips

- `gh` auto-detects the repo from the current directory
- Use `gh alias set` to create custom shortcuts
- `gh pr create --fill` auto-fills title from branch name
- Set `GH_EDITOR` env var to override editor per-session
- Use `--web` flag on most commands to open in browser

---

> **Full section:** [GitHub](../04-github/README.md) | **Next:** [Languages](languages-quick-reference.md)
