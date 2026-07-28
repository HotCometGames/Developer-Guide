# AI Development Quick Reference

> One-page reference for AI coding tools, prompt engineering, and context engineering. Print this or bookmark it.

---

## AI Coding Tools

### GitHub Copilot

| Action | How |
|--------|-----|
| Accept suggestion | `Tab` |
| Reject suggestion | `Esc` |
| Next suggestion | `Alt+]` |
| Previous suggestion | `Alt+[` |
| Inline chat | `Ctrl+I` |
| Open Copilot chat | `Ctrl+Shift+I` |
| Explain code | Select code → "Explain" |
| Fix errors | Select error → "Fix" |

### Cursor

| Action | How |
|--------|-----|
| Open AI chat | `Ctrl+L` |
| Inline edit | `Ctrl+K` |
| Accept edit | `Tab` |
| Reject edit | `Esc` |
| Add file to context | `@filename` |
| Add symbol | `#symbol` |
| Add docs | `@docs` |
| Generate from description | Describe in chat → generate |

### Common Agent Patterns

| Pattern | Description | When |
|---------|-------------|------|
| Code generation | Describe what you want | Building new features |
| Code explanation | Paste code, ask "explain" | Learning unfamiliar code |
| Refactoring | Select code → "refactor this" | Improving code quality |
| Bug fixing | Paste error, share context | Debugging |
| Test generation | "Write tests for this function" | Improving coverage |
| Documentation | "Document this function" | Writing docs |

## Prompt Engineering for Code

### Effective Prompts

| Instead of | Do |
|------------|-----|
| "Write a function" | "Write a Python function that takes a list of ints and returns the average, handling empty lists" |
| "Fix this bug" | "This function raises ValueError when input is empty. Fix it to return None instead" |
| "Make it better" | "Refactor this function to be more readable, extract helper functions" |
| "Write tests" | "Write pytest tests for edge cases: empty input, single element, negative numbers" |

### Prompt Structure

```
1. Context: What is this code/project?
2. Task: What do you want?
3. Constraints: Requirements, patterns, style
4. Examples: Show desired output format
5. Validation: How to verify it works
```

### Context Engineering

| Technique | How |
|-----------|-----|
| Provide file context | `@filename` or paste relevant files |
| Show examples | "Like this: [example]" |
| Specify language/framework | "In TypeScript with Express" |
| Reference existing code | "Follow the pattern in utils.ts" |
| State constraints | "Must work with Python 3.12+" |
| Show error output | Paste full error traceback |

## AGENTS.md Pattern

```markdown
# AGENTS.md

## Project
Brief description of the project.

## Build & Test
- `npm test` — run tests
- `npm run build` — build project

## Code Style
- Use TypeScript strict mode
- Prefer named exports
- Use functional components

## Architecture
- `src/api/` — API routes
- `src/lib/` — Business logic
- `src/components/` — React components
```

### Purpose

- Tells AI agents how to work with your codebase
- Provides context that isn't obvious from code alone
- Documents conventions that AI should follow
- Placed in repo root for global context

## AI-Assisted Workflows

### Feature Development

```
1. Describe feature to AI
2. AI generates initial implementation
3. Review and refine output
4. Write tests (AI-assisted)
5. Code review (human + AI)
6. Iterate on feedback
```

### Debugging

```
1. Share error message with AI
2. Share relevant code context
3. AI suggests possible causes
4. Test hypotheses
5. AI suggests fix
6. Verify fix works
7. Add regression test
```

### Code Review

```
1. Select changed code
2. Ask AI to review
3. AI flags potential issues
4. Discuss with team
5. Apply improvements
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Blindly accepting suggestions | Introduces bugs, security issues | Always review AI output |
| No context in prompt | Generic, unhelpful response | Provide file, error, and goal |
| Trusting AI for security | May generate vulnerable code | Manual security review |
| Using AI for all decisions | Loses critical thinking | Use as assistant, not oracle |
| Not verifying output | Silent failures | Always test generated code |
| Sharing secrets in prompts | Data leak risk | Sanitize inputs before sharing |

---

> **Full section:** [AI Development](../09-ai-development/README.md) | **Next:** [Game Development](gamedev-quick-reference.md)
