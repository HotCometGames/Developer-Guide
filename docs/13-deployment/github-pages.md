# GitHub Pages

> Free static site hosting directly from a GitHub repository.

> **Related:** [What Is Deployment?](what-is-deployment.md) | [CI/CD Pipelines](ci-cd-pipelines.md) | [GitHub Actions](../04-github/github-actions.md)

---

## What Is It?

GitHub Pages serves static files from a repository. It's ideal for documentation sites, personal pages, project landing pages, and any site that doesn't need a server-side runtime.

## Setup

### 1. Enable Pages

```
Repo Settings → Pages → Source → GitHub Actions
```

### 2. Create a Deploy Workflow

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  push:
    branches: ["master"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"
          cache: pip
      - run: pip install -r requirements.txt
      - run: mkdocs build
      - run: touch ./site/.nojekyll
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

### 3. Custom Domain

```
Repo Settings → Pages → Custom domain → yourdomain.com
```

Add a `CNAME` record pointing to `<user>.github.io` at your DNS provider.

## .nojekyll

GitHub Pages assumes Jekyll by default. A `.nojekyll` file in the output directory tells Pages not to process the site with Jekyll — needed for static site generators like MkDocs, Hugo, or plain HTML.

## Branch-Based Pages (Legacy)

```
Settings → Pages → Source → Deploy from a branch
```

This builds from `gh-pages` or a `/docs` folder on the default branch. **Prefer the GitHub Actions approach** above for more control.

## Best Practices

- **Use GitHub Actions for builds** — more control, cleaner cache, better error reporting
- **Add `.nojekyll`** — Jekyll processing can break non-Jekyll sites
- **Cache dependencies in CI** — `cache: pip` or `cache: npm` cuts build time significantly
- **Use `workflow_dispatch`** — allows manual re-deploy from the Actions tab

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| No `.nojekyll` | Files starting with `_` are hidden by Jekyll | Add `touch ./site/.nojekyll` to workflow |
| Pushing build artifacts | Build output in repo | Gitignore `site/` or build directory |
| Mixed content on HTTPS | Assets loaded over HTTP | Use `https://` for all external resources |
| Custom domain not propagating | DNS changes take time | Wait up to 24 hours, verify with `dig` |

## What's Next?

Learn more about [CI/CD Pipelines](ci-cd-pipelines.md) for other deployment targets, or see [Vercel](vercel.md) for frontend apps with serverless backends.
