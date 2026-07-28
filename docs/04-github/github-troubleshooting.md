# GitHub Troubleshooting

> Common GitHub errors and how to fix them.

> **Related:** [GitHub CLI](github-cli.md) | [GitHub Actions](github-actions.md) | [Git Troubleshooting](../03-git/git-troubleshooting.md)

---

## What Is This?

GitHub issues usually fall into a few categories: authentication, permissions, CI failures, and Pages deployment problems.

## Authentication

### "Support for password authentication was removed"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't push with password | GitHub deprecated password auth for HTTPS | Use a personal access token (classic or fine-grained) or SSH. Generate at **Settings → Developer settings → Personal access tokens** |
| `gh auth login` fails | Browser not available for OAuth | `gh auth login --with-token < token.txt` or `gh auth login -h github.com -p https` |

### "Permission denied (publickey)"

| Problem | Cause | Solution |
|---------|-------|----------|
| SSH key not recognized | Key not added to your GitHub account | Run `cat ~/.ssh/id_ed25519.pub`, add output at **Settings → SSH and GPG keys** |
| Wrong key used | Multiple SSH keys, wrong one selected | Use `ssh -T git@github.com` to test. Configure `~/.ssh/config` to specify the key |

```ssh-config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
```

## Permissions

### "You don't have permission to push to this branch"

| Problem | Cause | Solution |
|---------|-------|----------|
| Branch is protected | Branch protection rules prevent direct push | Open a PR instead. If you need direct access, request write/admin access |
| Not a collaborator | You don't have access to the repo | Fork the repo and submit a PR from your fork |

### "Resource not accessible by integration"

| Problem | Cause | Solution |
|---------|-------|----------|
| Action can't access a resource | GITHUB_TOKEN permissions are limited | Set explicit permissions in the workflow: `permissions: contents: read, issues: write` |
| Fork PR can't access secrets | Secrets are not shared to fork PRs | Workaround: use `pull_request_target` event (but review security implications) |

## Pull Requests

### "This branch has conflicts that must be resolved"

| Problem | Cause | Solution |
|---------|-------|----------|
| PR has merge conflicts | Both branches changed the same lines | Resolve via web editor (GitHub shows the conflicts), or locally: `git merge main` then `git push` |
| "This branch is out of date" | PR branch is behind base branch | Use **Update branch** button on the PR page, or `git merge main` locally |

### "Only those with write access can merge"

| Problem | Cause | Solution |
|---------|-------|----------|
| Merge button disabled | You don't have write access to the repo | Ask a maintainer to merge, or become a collaborator |

## Actions

### "Failed to upload artifact"

| Problem | Cause | Solution |
|---------|-------|----------|
| Artifact path doesn't exist | Build step didn't produce the expected files | Check the build step output. Does the folder exist? Is the path correct? |
| Artifact too large | >10 GB limit for artifacts | Reduce artifact size, split into multiple artifacts, or use external storage |

### "No hosted runners found"

| Problem | Cause | Solution |
|---------|-------|----------|
| Runner selection unavailable | Free tier runner quota exhausted | Wait for quota reset, switch to self-hosted runner, or upgrade plan |

### "The process '...' failed with exit code 1"

| Problem | Cause | Solution |
|---------|-------|----------|
| Command error | The script or command in a step failed | Click the failed step in the GitHub Actions UI to see the full error log |

## GitHub Pages

### "Site not published"

| Problem | Cause | Solution |
|---------|-------|----------|
| Pages not enabled | Pages not configured in repo settings | Go to **Settings → Pages** and select a source (branch or Actions) |
| Build fails in Actions | Workflow error | Check the Actions run logs. Common issues: missing `pages: write` permissions, wrong artifact path |

### "Your site is being built and published..."

| Problem | Cause | Solution |
|---------|-------|----------|
| Site is taking too long | Large site or slow build | Check Actions tab for progress. If stuck >10 minutes, cancel and re-run |

### Site shows raw HTML instead of rendered content

| Problem | Cause | Solution |
|---------|-------|----------|
| GitHub Pages runs Jekyll | Jekyll processes HTML through its pipeline | Add a `.nojekyll` file to your published content root |

## GitHub CLI

### "gh: command not found"

| Problem | Cause | Solution |
|---------|-------|----------|
| gh not installed | CLI not installed on your machine | Install: Windows: `winget install GitHub.cli`, macOS: `brew install gh`, Linux: `sudo apt install gh` |
| Not in PATH | Installation path not in PATH | Restart terminal or add to PATH manually |

### "You are not logged in"

| Problem | Cause | Solution |
|---------|-------|----------|
| Not authenticated | `gh` has no valid auth session | Run `gh auth login` or set `GITHUB_TOKEN` environment variable |

## General Diagnostics

| Command | What It Tells You |
|---------|-------------------|
| `gh auth status` | Are you authenticated? Which account? |
| `ssh -T git@github.com` | Is SSH configured correctly? |
| `gh api /repos/owner/repo` | Raw API response for a repo |
| `gh run list --limit 5` | Recent workflow runs and their status |
| `gh repo view owner/repo` | Repository details and description |
