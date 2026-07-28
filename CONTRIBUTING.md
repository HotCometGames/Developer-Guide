# Contributing to the Developer Handbook

This guide explains how to add and edit content in the Developer Handbook.

---

## Quick Start

1. Find the right section folder (e.g., `02-terminal/`)
2. Check the section `README.md` for existing pages
3. Use the appropriate template from `00-templates/`
4. Follow the [Style Guide](STYLE-GUIDE.md)
5. Add cross-links to related pages
6. Test all links and code examples

---

## Adding a New Page

### 1. Choose the Right Section

| Topic | Section |
|-------|---------|
| How computers work | `01-foundations/` |
| Terminal commands | `02-terminal/` |
| Git commands | `03-git/` |
| GitHub features | `04-github/` |
| Editor setup | `05-editors/` |
| Programming languages | `06-programming-languages/` |
| Package managers | `07-package-managers/` |
| Virtual environments | `08-virtual-environments/` |
| AI development tools | `09-ai-development/` |
| Architecture patterns | `10-software-architecture/` |
| Project management | `11-project-management/` |
| Testing | `12-testing/` |
| Deployment | `13-deployment/` |
| Game development | `14-game-development/` |
| Machine learning | `15-machine-learning/` |
| Hackathons | `16-hackathons-game-jams/` |
| Developer wisdom | `17-developer-wisdom/` |
| Cheat sheets | `18-cheat-sheets/` |

### 2. Pick a Template

Use the matching template from `00-templates/`:

- **Topic page:** `topic-page.md`
- **Cheat sheet:** `cheat-sheet.md`
- **Decision tree:** `decision-tree.md`
- **Checklist:** `checklist.md`

### 3. Name the File

- Use `lowercase-with-hyphens.md`
- Be descriptive: `powershell-vs-bash.md`, not `ps.md`
- Avoid abbreviations unless they're universally understood

### 4. Fill In the Template

Follow the canonical page structure from the [Style Guide](STYLE-GUIDE.md).

### 5. Update the Section README

Add your new page to the table in the section's `README.md`.

### 6. Add Cross-Links

- Link to your page from related pages in other sections
- Link from your page to related topics
- Update the section README's "Next" link if appropriate

---

## Editing an Existing Page

1. Read the page fully before editing
2. Preserve the existing structure and style
3. Test any code examples you add or change
4. Update cross-links if you change page titles or section names
5. Keep the page focused - if adding significant content, consider a new page

---

## Writing Standards

See the full [Style Guide](STYLE-GUIDE.md) for details.

### Key Rules

- **Markdown only** - No HTML unless absolutely necessary
- **Specify code language** - Always use ` ```powershell `, ` ```bash `, etc.
- **Relative links** - Use `../XX-section/page.md` for internal links
- **Tables for comparisons** - Use tables for command references and comparisons
- **Callouts for warnings** - Use `> **Warning:**` and `> **Tip:**` blockquotes
- **Mermaid for diagrams** - Use Mermaid for decision trees and workflows
- **Both platforms** - Show PowerShell and Bash equally for terminal topics

---

## Quality Checklist

Before submitting a page, verify:

- [ ] Follows the canonical template structure
- [ ] All code examples are correct and tested
- [ ] All internal links resolve correctly
- [ ] File name follows `lowercase-with-hyphens.md` convention
- [ ] Section README is updated with the new page
- [ ] Cross-links added from related pages
- [ ] No spelling or grammar errors
- [ ] Consistent formatting with other pages
- [ ] Both PowerShell and Bash shown (for terminal topics)
- [ ] Mermaid diagrams render correctly

---

## Templates

All templates are in `00-templates/`. Copy the appropriate template and fill in the sections.

| Template | Use For |
|----------|---------|
| `topic-page.md` | Standard topic documentation |
| `cheat-sheet.md` | One-page command/syntax reference |
| `checklist.md` | Step-by-step checklists |
| `project-plan.md` | Project planning documents |
| `feature-proposal.md` | Proposing new features |
| `bug-report.md` | Reporting bugs |
| `pull-request.md` | PR descriptions |
| `release-notes.md` | Version release notes |
| `meeting-notes.md` | Meeting documentation |
| `sprint-planning.md` | Sprint planning |
| `retrospective.md` | Sprint retrospectives |
| `architecture-decision-record.md` | Architecture decisions |
| `research-notes.md` | Research documentation |
| `design-document.md` | Design documents |
| `game-design-document.md` | Game design |
| `hackathon-planning.md` | Hackathon planning |
| `experiment-log.md` | Experiment tracking |

---

## Getting Help

- Check existing pages for style examples
- Review the [Style Guide](STYLE-GUIDE.md) for formatting rules
- Look at completed sections for reference
