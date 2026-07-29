# CI/CD Pipelines

> Automating the build, test, and deploy process so every change is validated and deliverable.

> **Related:** [GitHub Actions](../04-github/github-actions.md) | [What Is Deployment?](what-is-deployment.md) | [Environment Management](environment-management.md)

---

## What Is It?

CI/CD (Continuous Integration / Continuous Deployment) automates the software delivery pipeline. Every code push goes through a repeatable process: build → test → package → deploy.

## Pipeline Stages

```
┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
│   Lint   │ → │   Test   │ → │  Build   │ → │  Stage   │ → │  Deploy  │
│          │   │          │   │          │   │          │   │          │
│ prettier │   │ pytest   │   │ docker   │   │ push to  │   │ prod env │
│ ruff     │   │ jest     │   │ vite     │   │ staging  │   │          │
└──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
```

| Stage | Fast? | Purpose |
|-------|-------|---------|
| Lint | Yes | Catch formatting and style issues immediately |
| Test | Yes | Unit + integration tests |
| Build | Medium | Compile, bundle, create Docker image |
| Stage | Medium | Deploy to staging, run smoke/E2E tests |
| Deploy | Varies | Push to production |

## Gating

Each stage gates the next. If lint fails, don't run tests. If tests fail, don't build.

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps: [/* lint */]

  test:
    needs: lint          # only runs if lint passes
    runs-on: ubuntu-latest
    steps: [/* test */]

  build:
    needs: test          # only runs if tests pass
    runs-on: ubuntu-latest
    steps: [/* build */]
```

## Matrix Builds

Test across multiple versions or configurations in parallel:

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
    python-version: ["3.11", "3.12"]

steps:
  - uses: actions/setup-python@v5
    with:
      python-version: ${{ matrix.python-version }}
  - run: pytest
```

The matrix runs every combination: Ubuntu + 3.11, Ubuntu + 3.12, Windows + 3.11, Windows + 3.12 — in parallel.

## Build Once, Deploy Many

Build the artifact once in CI, then promote the same artifact through environments:

```
CI build → image:a1b2c3d
              ↓
         Deploy to staging  (image:a1b2c3d)
              ↓
         Smoke test staging
              ↓
         Deploy to production (the same image:a1b2c3d)
```

This guarantees that what you tested is exactly what you deploy.

## Artifact Passing

```yaml
- name: Upload build artifact
  uses: actions/upload-artifact@v4
  with:
    name: build-output
    path: dist/

# Later job
- name: Download build artifact
  uses: actions/download-artifact@v4
  with:
    name: build-output
```

## CI Triggers

| Trigger | Use Case |
|---------|----------|
| `push` to main | Deploy to production |
| `pull_request` | Validate before merging |
| `schedule` (cron) | Nightly tests, dependency updates |
| `workflow_dispatch` | Manual re-deploy |
| `push` to any branch | Lint + test only (no deploy) |

## Best Practices

- **Fast feedback** — lint and unit tests should complete in < 5 minutes
- **Fail fast** — stop the pipeline on the first failure
- **Deterministic builds** — same commit → same artifact, always
- **Immutable artifacts** — tag with the git SHA, never overwrite
- **Secrets in CI** — use CI secrets management, not plaintext in config
- **Cache dependencies** — pip/npm cache in CI cuts minutes per run

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Building in production | Different artifact than tested | Build once in CI, promote to prod |
| No test gating | Broken code gets deployed | Gate deploy on passing tests |
| Long-running pipelines | Developers ignore CI | Keep under 10 minutes |
| Hardcoded secrets in workflow | Secret leaks | Use `${{ secrets.X }}` |
| Deploying on every branch push | Too many deployments | Branch filter in trigger |

## What's Next?

Set up [Environment Management](environment-management.md) for secrets and config, or deploy to [GitHub Pages](github-pages.md), [Vercel](vercel.md), or [Railway](railway.md).
