# GitHub CLI

> The `gh` command-line tool brings GitHub to your terminal: repos, PRs, issues, Actions, and more.

> **Related:** [Pull Requests](pull-requests.md) | [GitHub Actions](github-actions.md) | [Git CLI](../03-git/collaboration.md)

---

## What Is It?

`gh` is GitHub's official CLI. It wraps the GitHub API so you can manage issues, pull requests, releases, Actions, and more without leaving the terminal. It complements Git — you still use `git` for version control and `gh` for GitHub-specific operations.

## Setup

```bash
gh auth login                    # authenticate with GitHub
gh auth status                   # verify authentication
gh config set editor "code --wait"
```

## Repository Operations

```bash
gh repo create name --public --clone   # create and clone
gh repo fork owner/repo --clone        # fork and clone
gh repo clone owner/repo               # clone without forking
gh repo view --web                     # open in browser
gh repo list                           # list your repos
gh repo set-default owner/repo         # set default remote
```

## Pull Requests

```bash
gh pr create --base main --title "Add login" --body "Closes #12"
gh pr create --draft                   # create as draft
gh pr list                             # list open PRs
gh pr list --state merged              # list merged PRs
gh pr view 42                          # view PR details
gh pr checkout 42                      # checkout PR locally
gh pr diff 42                          # show PR diff
gh pr review 42 --approve              # approve
gh pr review 42 --request-changes      # request changes
gh pr merge 42 --squash                # squash and merge
gh pr close 42                         # close without merging
gh pr ready 42                         # mark draft as ready
```

## Issues

```bash
gh issue create --title "Bug" --body "Description"
gh issue list                          # list open issues
gh issue list --label "bug"            # filter by label
gh issue list --assignee @me           # assigned to me
gh issue view 12                       # view issue details
gh issue close 12                      # close issue
gh issue reopen 12                     # reopen issue
```

## Actions

```bash
gh workflow list                       # list workflows
gh workflow run deploy                 # trigger workflow manually
gh run list                            # list recent runs
gh run view                            # view latest run
gh run watch                           # watch run in real-time
gh run rerun 123456                    # rerun a failed run
gh run download 123456                 # download artifacts
```

## Releases

```bash
gh release list                        # list releases
gh release create v1.0 --title "v1.0" --notes "Release notes"
gh release download v1.0               # download release assets
gh release view v1.0                   # view release details
gh release delete v1.0                 # delete a release
```

## Repo Management

```bash
gh repo edit --description "New desc" --visibility public
gh repo archive                        # archive the repo
gh repo rename new-name                # rename the repo
gh repo deploy-key list                # list deploy keys
gh repo list --limit 100               # list with limit
```

## Secrets

```bash
gh secret list                         # list repo secrets
gh secret set API_KEY                  # set a secret (prompts for value)
gh secret set API_KEY --body "value"   # set from command line
gh secret remove API_KEY               # remove a secret
```

## Gist

```bash
gh gist create file.txt                # create a gist
gh gist list                           # list your gists
gh gist view 123456                    # view a gist
gh gist edit 123456 file.txt           # edit a gist file
```

## Config & Help

```bash
gh config set git_protocol ssh         # use SSH instead of HTTPS
gh config set editor "code --wait"
gh help                                # general help
gh help pr create                      # help for a specific command
gh help environment                    # environment variables reference
```

## Aliases

```bash
gh alias set prs "pr list"
gh alias set co "pr checkout"
gh alias set bugs "issue list --label bug"
```

After setting aliases: `gh prs` lists PRs, `gh co 42` checks out PR 42.

## Key Differences from Git

| Task | Git | gh |
|------|-----|----|
| Clone repo | `git clone url` | `gh repo clone owner/repo` |
| Create PR | Push + web UI | `gh pr create` |
| List PRs | Web UI | `gh pr list` |
| View CI | Web UI | `gh run view` |
| Create issue | Web UI | `gh issue create` |
| Fork repo | Web UI | `gh repo fork` |
| View release | Web UI | `gh release view` |
