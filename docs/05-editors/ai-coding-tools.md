# AI Coding Tools

> AI-powered coding assistants that help you write, understand, and refactor code: Cursor, Codex CLI, and GitHub Copilot.

> **Related:** [AI Development](../09-ai-development/README.md) | [Editor Integrations](editor-integrations.md)

---

## What Is It?

AI coding tools integrate large language models directly into your editor. They can complete code as you type, generate functions from comments, explain code, and even autonomously implement features. These tools are changing how developers write software.

## Major Tools

| Tool | Type | Key Feature |
|------|------|-------------|
| **GitHub Copilot** | VS Code / JetBrains extension | Tab-to-complete autocomplete, chat, agent mode |
| **Cursor** | AI-first editor (fork of VS Code) | Multi-file editing, agent mode, full codebase context |
| **Codex CLI** | Terminal-based AI coding agent | Autonomous task execution, file editing, shell commands |
| **Claude Code** | Terminal-based AI coding agent | Deep reasoning, multi-step feature implementation |

## GitHub Copilot

Copilot provides inline code completions and a chat interface.

### Tab Completion

```
# Write a comment or function signature:
# function to calculate fibonacci sequence
def fibonacci(n):
    if n <= 1:        # ← Copilot suggests the next line
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```

Press **Tab** to accept, **Esc** to dismiss.

### Copilot Chat

**Ctrl+I** opens Copilot Chat inline. Ask questions about selected code, request refactors, or get explanations.

### Agent Mode

Describe a feature in natural language, and Copilot can:
- Create new files
- Edit multiple existing files
- Run terminal commands
- Fix errors automatically

## Cursor

Cursor is a fork of VS Code with deep AI integration. It understands your entire codebase.

### Key Features

- **Ctrl+K** — edit selected code by describing the change
- **Ctrl+L** — chat with full codebase context
- **Agent mode** — implements multi-step features across files
- **Composer** — edit multiple files simultaneously
- **AI Rules** — custom instructions for how AI should write code

### Codebase Awareness

Cursor indexes your project and understands:
- Project structure and conventions
- Type definitions and interfaces
- Function signatures and usage patterns
- Import/export relationships

## Codex CLI

Codex CLI is OpenAI's terminal-based coding agent. It runs in your terminal, reads your files, writes code, and executes commands.

```bash
# Start a Codex session in your project directory
codex
```

Codex CLI:
- Understands your project structure
- Implements features described in natural language
- Writes and edits files
- Runs tests and fixes failures
- Commits changes when done

It's designed for autonomous task execution rather than inline autocomplete.

## Choosing the Right Tool

| Use Case | Best Tool |
|----------|-----------|
| Fast inline completions | GitHub Copilot |
| Multi-file editing with context | Cursor |
| Autonomous task execution | Codex CLI or Claude Code |
| Terminal-first workflow | Claude Code or Codex CLI |
| VS Code integration | Copilot or Cursor |

## Best Practices

- **Be specific in prompts** — clear descriptions get better results
- **Always review AI-generated code** — AI can introduce bugs or security issues
- **Use context wisely** — include relevant files, error messages, and existing patterns
- **Start small** — ask for a single function before a whole feature
- **Iterate** — refine your prompt based on what the AI produces
- **Set project rules** — most tools support custom instructions for consistent code style

## What's Next?

For a deeper dive into AI-assisted development workflows, see [AI Development](../09-ai-development/README.md).
