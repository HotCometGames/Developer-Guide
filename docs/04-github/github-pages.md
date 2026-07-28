# GitHub Pages

> Deploy static websites directly from a GitHub repository — free, fast, and automatic.

> **Related:** [GitHub Actions](github-actions.md) | [Repositories](repositories.md)

---

## What Is It?

GitHub Pages hosts static websites from a GitHub repository. It's ideal for project documentation, personal sites, and landing pages. Pages integrates with Actions for full CI/CD deployment.

## How It Works

You push content to a branch (or use an Actions workflow), and GitHub serves it at a URL:

- **User/Org site:** `https://username.github.io`
- **Project site:** `https://username.github.io/repository-name`

## Setup Methods

### Method 1: Actions Workflow (Recommended)

The modern approach. Build your site with any static site generator and deploy via Actions:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install -r requirements.txt && mkdocs build
      - name: Create .nojekyll
        run: touch ./site/.nojekyll
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./site

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/deploy-pages@v4
```

1. Go to **Settings → Pages** → **Source** → **GitHub Actions**
2. Push the workflow file
3. Your site deploys automatically

### Method 2: Branch-Based

Push your static files to a special branch:

1. Go to **Settings → Pages** → **Source** → **Deploy from a branch**
2. Select branch (usually `gh-pages`) and folder (`/` or `/docs`)
3. Push your site content to that branch

### Method 3: /docs Folder

Keep your site files in a `/docs` folder on your main branch:

1. Go to **Settings → Pages** → **Source** → **Deploy from a branch**
2. Select `main` branch and `/docs` folder

## The .nojekyll File

GitHub Pages runs Jekyll by default. If you use a different static site generator (like MkDocs, Hugo, or plain HTML), create an empty `.nojekyll` file in the root of your published content:

```bash
touch .nojekyll
```

Without this, GitHub Pages may process your HTML through Jekyll, breaking paths and stripping content.

## Custom Domains

```bash
# Add a CNAME file to your repo
echo "example.com" > docs/CNAME
# or configure in Settings → Pages → Custom domain
```

Then add a DNS record:

| DNS Record | Type | Value |
|-----------|------|-------|
| apex | A | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| www | CNAME | `username.github.io` |

It may take up to 10 minutes for DNS to propagate. Check the **Settings → Pages** page for DNS verification.

## Enforcing HTTPS

In **Settings → Pages**, check **Enforce HTTPS**. GitHub automatically provisions a TLS certificate for your domain.

## 404 Pages

Create a `404.html` file in your site's root. GitHub Pages serves it automatically for any 404 error.

## Limitations

| Limitation | Detail |
|------------|--------|
| No server-side code | Static files only (HTML, CSS, JS) |
| Repository size | 1 GB recommended max |
| Build time | 10 minutes per workflow run |
| Bandwidth | 100 GB per month |
| Site size | 1 GB published max |

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Site shows raw HTML or plain text | Jekyll is processing your files | Add `.nojekyll` to your published content and redeploy |
| 404 on page load | Missing file or wrong path | Check repository file structure. If using a project site, the URL is `/repo-name/` |
| Custom domain not working | DNS not propagated | Verify DNS records with `dig` or `nslookup`, wait up to 10 minutes |
| Action fails to deploy | Missing Pages deployment permissions | Add `pages: write` and `id-token: write` permissions to workflow |
