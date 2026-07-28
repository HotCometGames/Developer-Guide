# Issues & Projects

> Track bugs, features, and tasks with GitHub Issues and organize work with Projects.

> **Related:** [Pull Requests](pull-requests.md) | [Repositories](repositories.md)

---

## What Is It?

Issues track individual tasks, bugs, feature requests, and questions. Projects provide a kanban-style board to organize issues across one or more repositories.

## Issues

### Creating an Issue

Click **Issues** → **New issue**, or use a template if one is configured.

Good issue structure:

```
**Description:**
What's happening and why.

**Steps to reproduce:**
1. Go to /login
2. Submit empty form
3. See crash

**Expected behavior:**
Show validation error message.

**Environment:**
- Browser: Chrome 120
- OS: Windows 11
```

### Via CLI

```bash
gh issue create --title "Login form crashes on empty submit" --body "Steps..."
```

### Labels

Categorize issues with labels:

| Label | Meaning |
|-------|---------|
| `bug` | Something isn't working |
| `enhancement` | New feature or request |
| `documentation` | Docs improvements |
| `good first issue` | Good for newcomers |
| `help wanted` | Looking for contributors |
| `question` | Needs clarification |

```bash
gh issue label list
gh issue label create "priority:high" --color "d93f0b"
```

### Milestones

Group issues by release or sprint:

```bash
gh issue list --milestone "v1.2"
```

| Task | Command |
|------|---------|
| Create issue | `gh issue create` |
| List issues | `gh issue list` |
| View issue | `gh issue view 42` |
| Close issue | `gh issue close 42` |
| Reopen issue | `gh issue reopen 42` |

### Issue Templates

In `.github/ISSUE_TEMPLATE/`, create YAML template files:

```yaml
name: Bug Report
description: Report a bug to help us improve
title: "[Bug]: "
labels: ["bug"]
body:
  - type: textarea
    id: description
    attributes:
      label: Description
      placeholder: What happened?
```

## Projects (Beta)

GitHub Projects provide a spreadsheet-like view of issues and PRs across repos.

### Views

| View | What It Shows |
|------|-------------|
| Table | Sortable, filterable spreadsheet of items |
| Board | Kanban columns by status, priority, or custom field |
| Roadmap | Timeline view by date field |

### Fields

Custom fields for tracking:

- **Status** — Todo, In Progress, Done
- **Priority** — Low, Medium, High, Urgent
- **Size** — XS, S, M, L, XL
- **Date** — Start date, due date
- **Iteration** — Sprint or time period

### Automating Projects

Use Actions or built-in workflows:

| Trigger | Action |
|---------|--------|
| Issue opened | Add to project, set status "Todo" |
| PR merged | Move to "Done", add to "Shipped" iteration |
| PR opened | Set status "In Review" |

### Via CLI

```bash
gh project list                   # list projects for the current repo
gh project item-add 1 --owner "org" --url "https://github.com/..."  # add item
```

## Best Practices

- **One issue per problem** — don't bundle unrelated topics
- **Use templates** — consistent, complete bug reports
- **Link PRs to issues** — auto-close when merged
- **Keep the board current** — stale boards lose trust
- **Use labels sparingly** — too many labels become noise
- **Set milestones for releases** — track progress toward ship dates
