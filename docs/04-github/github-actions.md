# GitHub Actions

> Automate builds, tests, deployments, and anything else with GitHub's CI/CD platform.

> **Related:** [GitHub Pages](github-pages.md) | [Pull Requests](pull-requests.md)

---

## What Is It?

GitHub Actions lets you run automated workflows in response to GitHub events: push, PR, issue creation, schedule, and more. It's CI/CD, task automation, and infrastructure all in one.

## Core Concepts

| Concept | What It Is |
|---------|------------|
| **Workflow** | An automated process defined in `.github/workflows/*.yml` |
| **Job** | A set of steps that run on the same runner |
| **Step** | An individual task: run a script or action |
| **Action** | A reusable unit of automation (community or custom) |
| **Runner** | A virtual machine or self-hosted server that runs jobs |
| **Event** | What triggers the workflow (push, pull_request, schedule) |

## Anatomy of a Workflow

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:       # manual trigger

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"
      - run: pip install -r requirements.txt
      - run: pytest
```

## Common Triggers

```yaml
on:
  push:                               # on every push
    branches: [main, develop]          # only these branches
    paths: ['src/**', 'tests/**']      # only if these paths change
  pull_request:
    types: [opened, synchronize]       # new PR or new commit to PR
  schedule:
    - cron: '0 6 * * 1'               # every Monday at 6 AM UTC
  workflow_dispatch:                   # manual trigger (button in UI)
  release:
    types: [published]                 # when a release is published
```

## Using Marketplace Actions

Browse [github.com/marketplace?type=actions](https://github.com/marketplace?type=actions) for reusable actions:

| Action | Purpose |
|--------|---------|
| `actions/checkout` | Check out your repository |
| `actions/setup-python` | Install Python |
| `actions/setup-node` | Install Node.js |
| `actions/cache` | Cache dependencies for faster runs |
| `actions/upload-artifact` | Store build outputs |
| `actions/deploy-pages` | Deploy to GitHub Pages |

## Matrix Builds

Test against multiple versions or configurations:

```yaml
jobs:
  test:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        python-version: ["3.10", "3.11", "3.12"]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      - run: pytest
```

## Environment Variables and Secrets

```yaml
steps:
  - run: echo "Branch: ${{ github.ref_name }}"
    env:
      API_KEY: ${{ secrets.API_KEY }}
```

Store secrets in **Settings → Secrets and variables → Actions**.

## Caching Dependencies

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('requirements.txt') }}
```

## Self-Hosted Runners

Run workflows on your own hardware:

```bash
# On your machine, follow the setup instructions in Settings → Actions → Runners
./config.sh --url https://github.com/org/repo --token TOKEN
./run.sh
```

Then target it in workflows:

```yaml
runs-on: self-hosted
```

## Debugging

| Technique | How |
|-----------|-----|
| View logs | GitHub UI → Actions → workflow run → job |
| Re-run failed jobs | Click **Re-run jobs** (all or failed only) |
| Enable debug logging | Set secret `ACTIONS_STEP_DEBUG=true` |
| SSH to runner | Use `mxschmitt/action-tmate@v3` for live debugging |

## Best Practices

- **Pin action versions** — use `@v4` not `@main` to avoid surprise breakage
- **Keep workflows fast** — use caching and matrix builds wisely
- **Fail fast** — order steps so cheap checks run before expensive ones
- **Use concurrency** — cancel duplicate runs on the same branch
- **Test locally** — use `act` to run workflows locally before pushing
- **Secure secrets** — never log or echo secrets
