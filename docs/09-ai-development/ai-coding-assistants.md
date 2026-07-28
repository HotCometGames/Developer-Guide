# AI Coding Assistants

> Deep dive into the major AI coding tools — GitHub Copilot, Cursor, Windsurf, and Cline. Features, setup, and how to choose.

---

## What Are AI Coding Assistants?

AI coding assistants are tools that integrate language models directly into your development environment. They can suggest code as you type, answer questions about your codebase, rewrite selected code, and in some cases act autonomously to complete multi-file tasks.

> **Related:** [What Is AI Development?](what-is-ai-development.md) for the foundational mental model.

---

## GitHub Copilot

### What It Is

GitHub Copilot is an AI pair programmer that integrates with VS Code, JetBrains, Neovim, and other editors. It provides inline code suggestions as you type and a chat interface for questions.

### Setup

```bash
# VS Code
# Install "GitHub Copilot" extension from marketplace
# Sign in with your GitHub account

# JetBrains
# Settings → Plugins → GitHub Copilot

# Neovim
# Use copilot.vim plugin
```

### Key Features

| Feature | How | Use Case |
|---------|-----|----------|
| **Inline suggestions** | Start typing | Real-time code completion |
| **Next edit suggestions** | After making a change | Predicts your next edit |
| **Chat** | `Ctrl+Shift+I` | Ask questions about code |
| **Inline chat** | `Ctrl+I` | Edit code with instructions |
| **Explain** | Select code → "Explain" | Understand unfamiliar code |
| **Fix** | Select error → "Fix" | Debug errors |
| **Tests** | "Write tests" | Generate test cases |
| **PR review** | In PR view → "Review" | Review pull requests |

### Keyboard Shortcuts (VS Code)

| Action | Shortcut |
|--------|----------|
| Accept suggestion | `Tab` |
| Reject suggestion | `Esc` |
| Next suggestion | `Alt+]` |
| Previous suggestion | `Alt+[` |
| Inline chat | `Ctrl+I` |
| Open chat panel | `Ctrl+Shift+I` |

### Customization

```json
// settings.json
{
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": true
  },
  "github.copilot.editor.enableCodeActions": true
}
```

### Pricing

| Plan | Cost | Includes |
|------|------|----------|
| Individual | $10/mo | Code completions + chat |
| Business | $19/user/mo | Organization policies, audit logs |
| Enterprise | $39/user/mo | Knowledge base, model selection |

---

## Cursor

### What It Is

Cursor is a VS Code fork built around AI. It has native chat, inline editing, and an agent mode that can read your entire codebase and make multi-file changes.

### Setup

```bash
# Download from cursor.com
# It's a standalone app (VS Code fork)
# Import your VS Code settings automatically
```

### Key Features

| Feature | How | Use Case |
|---------|-----|----------|
| **Chat** | `Ctrl+L` | Ask questions, generate code |
| **Inline edit** | `Ctrl+K` | Rewrite selected code |
| **Agent mode** | Chat → toggle Agent | Multi-file autonomous changes |
| **Composer** | `Ctrl+I` | Plan and execute complex changes |
| **@-mentions** | `@filename` | Reference specific files |
| **#-symbols** | `#symbolName` | Reference specific functions/classes |
| **@-docs** | `@docs` | Reference documentation |
| **@-web** | `@web` | Search the web for context |

### Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Open chat | `Ctrl+L` |
| Inline edit | `Ctrl+K` |
| Accept edit | `Tab` |
| Reject edit | `Esc` |
| Toggle agent | In chat panel |
| Open composer | `Ctrl+I` |

### Rules Files

Cursor supports rules that persist across conversations:

```markdown
// .cursor/rules/my-project.mdc
---
description: Project conventions
globs: ["*.ts", "*.tsx"]
---
- Use TypeScript strict mode
- Prefer named exports
- Use functional components with hooks
- Follow existing patterns in src/
```

### Pricing

| Plan | Cost | Includes |
|------|------|----------|
| Free | $0 | 50 slow completions + 50 chat messages |
| Pro | $20/mo | 500 fast completions + unlimited chat |
| Business | $40/user/mo | Org management, privacy mode |

---

## Windsurf

### What Is It

Windsurf (formerly Codeium) is an AI editor with "Cascade" — an agent that understands your codebase and can make multi-file changes with full context.

### Key Features

| Feature | Description |
|---------|-------------|
| **Cascade** | Agent that plans and executes multi-file changes |
| **Flows** | Step-by-step execution with checkpoints |
| **Context awareness** | Automatically finds relevant files |
| **Inline suggestions** | Autocomplete as you type |
| **Chat** | Ask questions about your code |

### Pricing

| Plan | Cost | Includes |
|------|------|----------|
| Free | $0 | Basic completions + limited Cascade |
| Pro | $15/mo | Unlimited completions + Cascade |
| Teams | $30/user/mo | Org features, audit logs |

---

## Cline

### What Is It

Cline is a VS Code extension that acts as an autonomous coding agent. It can read files, write code, run terminal commands, and use the browser — all with your approval at each step.

### Key Features

| Feature | Description |
|---------|-------------|
| **Autonomous execution** | Plans and executes multi-file changes |
| **Tool use** | Reads files, writes code, runs commands |
| **Browser control** | Can open and interact with web pages |
| **MCP support** | Connects to external tools via Model Context Protocol |
| **Step-by-step approval** | You approve each action before it runs |

### Setup

```bash
# VS Code
# Install "Cline" extension from marketplace
# Configure API key (Claude, GPT-4, etc.)
```

### Pricing

BYOK (Bring Your Own Key) — you pay for API usage directly.

---

## Comparison

| Feature | Copilot | Cursor | Windsurf | Cline |
|---------|---------|--------|----------|-------|
| **Type** | Plugin | Standalone IDE | Standalone IDE | Plugin |
| **IDE** | VS Code, JetBrains, Neovim | Cursor (VS Code fork) | Windsurf (VS Code fork) | VS Code |
| **Inline suggestions** | Best-in-class | Good | Good | Basic |
| **Chat** | Yes | Yes | Yes | Yes |
| **Inline edit** | Yes (`Ctrl+I`) | Yes (`Ctrl+K`) | Yes | Yes |
| **Agent mode** | Copilot Workspace | Yes | Cascade | Yes (native) |
| **Codebase awareness** | Good | Best | Good | Good |
| **Rules/config** | Custom instructions | .cursor/rules | .windsurfrules | .clinerules |
| **MCP support** | No | Yes | Yes | Yes |
| **Pricing model** | Subscription | Subscription | Subscription | BYOK |
| **Cost** | $10-39/mo | $0-40/mo | $0-30/mo | API costs only |

## How to Choose

### Start Here

- **New to AI coding?** → GitHub Copilot (lowest friction, best autocomplete)
- **Want codebase-aware chat?** → Cursor (best context, @-mentions)
- **Want autonomous agents?** → Cline or Cursor Agent (most control)
- **Budget-conscious?** → Copilot Free + Cline (BYOK)

### Upgrade When

- Copilot suggestions aren't contextual enough → Try Cursor
- You need multi-file refactoring → Try Cursor Agent or Cline
- You want to connect external tools → Try Cline with MCP

## Best Practices

- **Start with one tool** — Master it before adding more
- **Learn the shortcuts** — Speed comes from keyboard, not mouse
- **Use rules files** — AGENTS.md, .cursorrules — they improve suggestions dramatically
- **Review diffs carefully** — Especially with agent mode
- **Combine tools** — Copilot for autocomplete + Cursor for chat is a common setup

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Using all tools at once | Conflicting suggestions, context loss | Pick one primary tool |
| Ignoring rules files | Generic suggestions | Configure .cursorrules or AGENTS.md |
| Not learning shortcuts | Slow, mouse-heavy workflow | Learn 5 key shortcuts per tool |
| Trusting agent mode blindly | May make wrong architectural decisions | Review each change |
| Paying for features you don't use | Wasted money | Audit your plan quarterly |

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| No suggestions appearing | Extension disabled or not signed in | Check extension status, re-auth |
| Suggestions are generic | No codebase context | Use @-mentions, add rules file |
| Agent makes wrong changes | Insufficient context | Provide more files, be specific |
| Tool is slow | Large codebase, network issues | Use .gitignore exclusions, check connection |
| Suggestions don't match style | No style rules configured | Add coding conventions to rules file |

## Related Topics

- [Prompt Engineering](prompt-engineering.md) - Getting better output from any tool
- [Context Engineering](context-engineering.md) - Managing what AI can see
- [AI Agents](ai-agents.md) - Deep dive into agent capabilities

## Further Learning

- [GitHub Copilot Docs](https://docs.github.com/en/copilot) - Official documentation
- [Cursor Docs](https://docs.cursor.com) - Official Cursor guide
- [Windsurf Docs](https://docs.windsurf.com) - Official Windsurf guide
- [Cline Docs](https://docs.cline.bot) - Official Cline guide

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
