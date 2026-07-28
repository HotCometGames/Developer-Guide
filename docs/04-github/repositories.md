# Repositories

> Creating, managing, and organizing Git repositories on GitHub.

> **Related:** [What Is GitHub?](what-is-github.md) | [Pull Requests](pull-requests.md)

---

## What Is It?

A repository (repo) on GitHub is a remote copy of your Git repository with extra features: a web UI, issue tracker, wiki, and collaboration settings.

## Creating a Repository

### Via the Web

1. Click the **+** icon → **New repository**
2. Fill in:
   - **Owner** — your account or an organization
   - **Repository name** — short, descriptive, kebab-case
   - **Description** — optional, but helpful
   - **Visibility** — Public (anyone can see) or Private (you choose)
   - **Initialize with** — README, .gitignore template, license
3. Click **Create repository**

### Via the CLI

```bash
gh repo create my-project --public --clone
```

Creates the repo on GitHub and clones it locally in one command.

## Cloning a Repository

```bash
git clone https://github.com/user/repo.git
# or with gh:
gh repo clone user/repo
```

## Repository Structure

A well-organized repo typically has:

```
.
├── .github/            # GitHub-specific config (workflows, templates, CODEOWNERS)
├── docs/               # Documentation
├── src/                # Source code
├── tests/              # Tests
├── .gitignore          # Files Git should ignore
├── README.md           # Project overview
├── LICENSE             # License file
└── CONTRIBUTING.md     # Contribution guide
```

### .github/ Directory

Special directory for GitHub-specific files:

| File | Purpose |
|------|---------|
| `workflows/*.yml` | GitHub Actions workflows |
| `ISSUE_TEMPLATE/*.yml` | Issue templates |
| `PULL_REQUEST_TEMPLATE.md` | PR template |
| `CODEOWNERS` | Auto-assign reviewers |
| `dependabot.yml` | Dependency update config |

## Repository Settings

| Setting | What It Does |
|---------|-------------|
| Visibility | Public, Private, or Internal |
| Default branch | Usually `main` |
| Branch protection | Require PRs, passing checks, or reviews before merge |
| Topics | Labels that help others discover your repo |
| Collaborators | Add people with read, write, or admin access |
| Pages | Enable GitHub Pages for this repo |

## Forking

A fork is a copy of someone else's repository under your account. It links back to the original (upstream) so you can sync changes and submit Pull Requests.

```bash
gh repo fork owner/repo --clone
```

## Managing Multiple Repos

### Organizations

Group repos under an organization account for teams:

- **Teams** — manage access with role-based groups
- **Projects** — cross-repo project boards
- **Audit log** — track actions across the org

### Topics and Search

Tag repos with topics for discoverability:

```
github.com/search?q=topic:game-engine+topic:rust
```

## Best Practices

- **Write a good README** — what, why, how, and how to contribute
- **Add a license** — determine how others can use your code
- **Use branch protection** — prevent direct pushes to `main`
- **Set up .gitignore** — don't commit unnecessary files
- **Keep repos focused** — one project per repo
