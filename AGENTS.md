# Developer Guide — AGENTS.md

MkDocs-based personal engineering reference manual. Deployed to GitHub Pages.

## Commands

```bash
pip install -r requirements.txt   # install MkDocs + Material theme
mkdocs serve                       # dev server → http://127.0.0.1:8000
mkdocs build                       # static build output → site/ (gitignored)
```

## Structure

- Content: `docs/` → `00-templates/`, `01-foundations/` … `18-cheat-sheets/`
- Config: `mkdocs.yml` — update both `nav:` and section `README.md` when adding pages
- Styles: `docs/stylesheets/custom.css`
- Templates: `docs/00-templates/` (20 templates including `agents-md.md`)

## Conventions

- Pages: `lowercase-with-hyphens.md` | Folders: `XX-topic-name/`
- Internal links: `../XX-section/page.md`
- Code blocks always specify language (e.g., `` ```powershell ``, `` ```bash ``)
- Mermaid for diagrams; admonition blockquotes for callouts
- Both PowerShell **and** Bash shown for terminal topics
- No tests, no linter, no typecheck — pure docs

## Git / CI

- Default branch: `master`
- Push to `master` → `.github/workflows/deploy.yml` builds & deploys to GitHub Pages
- Repo: `https://github.com/HotCometGames/Developer-Guide`
- Site: `https://hotcometgames.github.io/Developer-Guide/`

## Key Reference Files

- `HOW-TO-RUN.md`, `CONTRIBUTING.md`, `STYLE-GUIDE.md`, `.github/workflows/deploy.yml`
