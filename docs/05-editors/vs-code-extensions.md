# VS Code Extensions

> Essential VS Code extensions organized by category for every development workflow.

> **Related:** [VS Code Setup](vs-code-setup.md) | [Productivity & Customization](productivity.md)

---

## What Is It?

Extensions add language support, tools, themes, and workflows to VS Code. Thousands are available in the marketplace, but installing too many slows down the editor. This page covers the essential few.

## By Category

### Language Support

| Extension | Purpose |
|-----------|---------|
| Python | Language support, debugging, Jupyter |
| ESLint | JavaScript/TypeScript linting |
| Prettier | Code formatter (JS, TS, HTML, CSS, Markdown) |
| rust-analyzer | Rust language support |
| C# Dev Kit | C# and .NET support |
| GitHub Copilot | AI code completion |

### Git & GitHub

| Extension | Purpose |
|-----------|---------|
| GitLens | Inline blame, history, code lens |
| Git History | View log, compare branches |
| GitHub Pull Requests | Review and manage PRs from within VS Code |

### General Productivity

| Extension | Purpose |
|-----------|---------|
| Error Lens | Inline error messages |
| Code Spell Checker | Catch typos in code |
| Path Intellisense | Auto-complete file paths |
| Material Icon Theme | File type icons |
| Bracket Pair Colorizer | Color-matched bracket pairs (built-in in recent versions) |

### Testing & Debugging

| Extension | Purpose |
|-----------|---------|
| Test Explorer UI | Run tests from a sidebar |
| Live Share | Collaborative debugging |
| Thunder Client | REST API testing |
| REST Client | Send HTTP requests from `.http` files |

### Markdown & Docs

| Extension | Purpose |
|-----------|---------|
| Markdown All in One | Table of contents, shortcuts, auto-preview |
| Markdown Preview Enhanced | Richer Markdown preview |
| Draw.io Integration | Edit diagrams in VS Code |

### Game Development

| Extension | Purpose |
|-----------|---------|
| Unity | C# editing for Unity (via C# Dev Kit) |
| Godot Tools | GDScript and Godot project support |
| Shader languages | GLSL, HLSL syntax highlighting |
| Tiled | Tiled map editor integration |

### Themes

| Theme | Type |
|-------|------|
| One Dark Pro | Dark (most popular) |
| Dracula Official | Dark |
| Catppuccin | Dark/Light |
| Tokyo Night | Dark |
| GitHub Theme | Light/Dark |
| Nord | Minimal dark |

## How to Install

```bash
code --install-extension ms-python.python
code --install-extension eamodio.gitlens
code --install-extension github.copilot
```

Or browse the Extensions view in VS Code (**Ctrl+Shift+X**).

## Recommended Extension Packs

| Pack | Includes |
|------|----------|
| **Python starter** | Python, Pylance, Jupyter, Python Test Explorer |
| **Web dev** | ESLint, Prettier, Path Intellisense, Auto Rename Tag |
| **Game dev** | C# Dev Kit, Shader languages, Tiled, Godot Tools |
| **Git power** | GitLens, Git History, GitHub Pull Requests |
| **Docs** | Markdown All in One, Code Spell Checker, Draw.io |

## Managing Extensions

- **Disable per workspace** — right-click an extension → Disable (Workspace)
- **Sync across machines** — use Settings Sync
- **Profiles** — create different extension sets for different work types
- **Check for updates** — Extensions view → ... → Check for Extension Updates

## What to Avoid

- **Too many extensions** — each one adds startup time. Keep it under 20-30
- **Duplicate functionality** — Prettier and Beautify do the same thing
- **Unmaintained extensions** — check the last update date before installing
- **Themes + icon packs from unknown publishers** — stick to well-known ones
