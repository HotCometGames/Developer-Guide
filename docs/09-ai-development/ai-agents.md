# AI Agents

> What agents are, how they work, and how to use autonomous coding capabilities safely and effectively.

---

## What Are AI Agents?

An AI agent is a language model that can **use tools** — read files, write code, run terminal commands, search the web, and interact with APIs. Unlike chat (which just generates text), agents take actions in the real world.

> **Related:** [AI Coding Assistants](ai-coding-assistants.md) for tool-specific agent features. [Context Engineering](context-engineering.md) for managing what agents can see.

---

## Why Do They Exist?

Some tasks are too complex for a single prompt:

- "Refactor the authentication system to use JWT instead of sessions"
- "Add a new API endpoint with database migration, validation, and tests"
- "Port this module from JavaScript to TypeScript"

These require reading multiple files, understanding relationships, making changes across the codebase, and verifying the result. Agents can do this autonomously.

## Mental Model

Think of an agent as a **developer pair-programming with you**. They can:

```mermaid
graph TD
    A[Agent] --> B[Read Files]
    A --> C[Write Code]
    A --> D[Run Commands]
    A --> E[Search Codebase]
    A --> F[Use Browser]
    B --> G[Understand Context]
    C --> G
    D --> G
    E --> G
    F --> G
    G --> H[Make Changes]
    H --> I[Verify Result]
```

The key difference from chat: **agents can act, not just suggest**.

## Agent Capabilities

| Capability | What It Does | Example |
|------------|--------------|---------|
| **Read files** | Understands codebase structure | Reads `src/` to find patterns |
| **Write code** | Creates or modifies files | Adds new component, updates types |
| **Run commands** | Executes terminal commands | Runs tests, builds project |
| **Search** | Finds relevant code | Searches for similar patterns |
| **Browser** | Opens and reads web pages | Fetches documentation |
| **Multi-file** | Coordinates changes across files | Refactors across 10+ files |

## Agent Modes by Tool

### Cursor Agent

| Feature | How |
|---------|-----|
| Activate | Toggle "Agent" in chat panel |
| Read files | Automatic based on your request |
| Write files | Proposes changes, you accept/reject |
| Run commands | Proposes commands, you approve |
| Multi-file | Plans steps, executes sequentially |

**Best for:** Refactoring, feature development, bug fixes

### GitHub Copilot Workspace

| Feature | How |
|---------|-----|
| Activate | From issue → "Open in Copilot Workspace" |
| Plan | Generates implementation plan |
| Edit | Proposes code changes |
| Review | Shows diff for each file |
| Fix | Automatically addresses CI failures |

**Best for:** Issue-driven development, known tasks

### Cline

| Feature | How |
|---------|-----|
| Activate | Install extension, start chatting |
| Read files | Reads as needed for context |
| Write files | Writes with your approval |
| Run commands | Executes with your approval |
| Browser | Can open and interact with web pages |
| MCP | Connects to external tools |

**Best for:** Autonomous tasks, research, complex workflows

### Continue

| Feature | How |
|---------|-----|
| Activate | Install extension, configure models |
| Chat | Ask questions, get code |
| Edit | Select code, describe changes |
| Terminal | Run commands from chat |

**Best for:** Open-source, customizable, self-hosted

## The Agent Loop

```mermaid
graph TD
    A[1. You describe task] --> B[2. Agent plans steps]
    B --> C[3. Agent reads files]
    C --> D[4. Agent writes code]
    D --> E[5. Agent runs commands]
    E --> F{6. Success?}
    F -->|Yes| G[7. You review]
    F -->|No| H[Agent retries/fixes]
    H --> D
    G --> I{8. Accept?}
    I -->|Yes| J[Done]
    I -->|No| K[Provide feedback]
    K --> B
```

### Your Role in the Loop

| Step | Agent Does | You Do |
|------|-----------|--------|
| 1 | Listens | Describe what you want |
| 2 | Plans | Verify the plan makes sense |
| 3 | Reads | Ensure it reads the right files |
| 4 | Writes | Review each file change |
| 5 | Tests | Verify tests pass |
| 6 | Fixes | Approve or redirect |
| 7 | Presents | Final review |
| 8 | Waits | Accept or reject |

## MCP (Model Context Protocol)

### What Is It?

MCP is a standard for connecting AI agents to external tools and data sources. Think of it as **USB for AI** — a universal way to plug in new capabilities.

| Without MCP | With MCP |
|-------------|----------|
| Agent can only use built-in tools | Agent can use any MCP-connected tool |
| Limited to file/code/terminal | Can access databases, APIs, services |
| Manual integration for each tool | Standard protocol, plug and play |

### How It Works

```
Agent ←→ MCP Client ←→ MCP Server ←→ External Tool
                                      (Database, API, Browser, etc.)
```

### Common MCP Servers

| Server | Connects To | Use Case |
|--------|-------------|----------|
| Filesystem | Local files | Enhanced file access |
| GitHub | GitHub API | PRs, issues, repos |
| PostgreSQL | PostgreSQL DB | Query data, inspect schema |
| Puppeteer | Web browser | Web scraping, testing |
| Slack | Slack API | Send messages, read channels |

### Setting Up MCP

```json
// .cursor/mcp.json (Cursor)
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-token"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://localhost/mydb"]
    }
  }
}
```

## When to Use Agents vs Inline Suggestions

| Use Inline Suggestions When | Use Agents When |
|-----------------------------|-----------------|
| Completing a line or block | Multi-file changes |
| Small, local edits | Refactoring across modules |
| Quick fixes | Adding new features with tests |
| You know exactly what to write | You need help figuring out the approach |
| Low risk, easily reversible | Complex, interconnected changes |

## Safety Guidelines

### The Golden Rule

**Always review agent output before committing.** Agents can:

- Delete files you didn't intend to delete
- Introduce subtle logic errors
- Run commands with unintended side effects
- Modify files outside the scope of the task

### Safety Checklist

- [ ] Review every file change before accepting
- [ ] Check that tests still pass
- [ ] Verify the agent didn't modify unrelated files
- [ ] Check for security issues (hardcoded secrets, vulnerable patterns)
- [ ] Test the feature manually if possible
- [ ] Commit only after thorough review

### Scoped Tasks

Good agent tasks are **bounded**:

| Good (Scoped) | Bad (Unscoped) |
|----------------|----------------|
| "Add a `validateEmail` function to `src/utils.ts`" | "Improve the codebase" |
| "Refactor `UserService` to use dependency injection" | "Make the code better" |
| "Add error handling to the API routes in `src/routes/`" | "Fix all bugs" |
| "Port `utils.ts` to TypeScript" | "Convert the whole project to TypeScript" |

## Best Practices

- **Start with a plan** — Ask the agent to outline its approach before coding
- **Scope tightly** — One feature, one refactor, one bug fix per agent session
- **Review diffs** — Don't just look at the final result, review each change
- **Test after** — Run your test suite after agent changes
- **Use rules files** — AGENTS.md and .cursorrules guide the agent
- **Keep conversations focused** — Start new sessions for new tasks

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Trusting agent output blindly | Bugs, security issues | Always review changes |
| Unscoped tasks | Agent modifies unrelated code | Break into small, focused tasks |
| Not reviewing file changes | Subtle modifications missed | Check every file diff |
| Running agents on production | Destructive changes | Use dev branches |
| No test suite | Can't verify changes work | Add tests before using agents |
| Ignoring agent plan | Agent goes off track | Review plan before execution |

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Agent modifies wrong files | Task too broad | Narrow scope, specify exact files |
| Agent runs destructive commands | No guardrails | Review commands before approval |
| Agent loops endlessly | Conflicting instructions | Start new conversation, clarify goal |
| Agent can't find relevant code | No context | Use rules files, @-mentions |
| Agent output is low quality | Insufficient context | Provide more files, clearer constraints |

## Related Topics

- [AI Coding Assistants](ai-coding-assistants.md) - Tool-specific agent features
- [Context Engineering](context-engineering.md) - Managing what agents can see
- [Workflows](ai-workflows.md) - Putting it all together

## Further Learning

- [Model Context Protocol](https://modelcontextprotocol.io/) - Official MCP docs
- [Cursor Agent Docs](https://docs.cursor.com/agent) - Cursor agent guide
- [Cline Docs](https://docs.cline.bot) - Cline agent guide

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
