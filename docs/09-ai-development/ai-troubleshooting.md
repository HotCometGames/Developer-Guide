# AI Troubleshooting

> Common issues with AI coding tools and how to fix them. Tool-specific problems, quality issues, and performance fixes.

---

## What Is It?

This page covers practical solutions for problems you'll encounter when using AI coding assistants. From suggestions not appearing to agents making wrong changes.

> **Related:** [AI Coding Assistants](ai-coding-assistants.md) for tool setup. [Context Engineering](context-engineering.md) for improving suggestions.

---

## Tool Issues

### GitHub Copilot

| Problem | Cause | Solution |
|---------|-------|----------|
| No suggestions appearing | Extension disabled | Check Extensions panel, enable Copilot |
| Not signed in | Auth expired | Sign out and sign back in |
| Suggestions are generic | No codebase context | Add `.github/copilot-instructions.md` |
| Slow suggestions | Network issues | Check connection, try VPN off |
| Wrong language suggestions | Language not enabled | Enable in Copilot settings |
| Suggestions ignore style | No style rules | Add coding conventions to instructions |

### Cursor

| Problem | Cause | Solution |
|---------|-------|----------|
| Chat doesn't see my code | Files not in context | Use `@filename` to reference files |
| Agent modifies wrong files | Task too broad | Narrow scope, specify exact files |
| Rules not applied | Rules file missing or wrong path | Check `.cursor/rules/` directory |
| Slow responses | Large context, network | Reduce context, check connection |
| Composer won't start | Extension issue | Restart Cursor, reinstall extension |
| Can't find symbol | Not indexed | Use `#symbolName` after indexing |

### Windsurf

| Problem | Cause | Solution |
|---------|-------|----------|
| Cascade doesn't understand context | Insufficient files referenced | Add more context to conversation |
| Slow cascade | Large codebase | Narrow the task scope |
| Rules not loading | Wrong file location | Check `.windsurfrules` in project root |

### Cline

| Problem | Cause | Solution |
|---------|-------|----------|
| Won't connect to API | Invalid API key | Check API key in settings |
| Agent loops endlessly | Conflicting instructions | Start new conversation, clarify goal |
| Won't run commands | Permission settings | Check tool permission configuration |
| High API costs | Too many iterations | Scope tasks more tightly |

## Quality Issues

### Bad Suggestions

| Symptom | Cause | Solution |
|---------|-------|----------|
| Generic boilerplate | No context provided | Add rules files, reference specific files |
| Wrong library used | No stack context | Specify your tech stack in rules |
| Doesn't match style | No style conventions | Add coding style to `.cursorrules` |
| Ignores constraints | Too many constraints | Lead with the most important constraint |
| Uses deprecated APIs | Training data outdated | Specify current versions, reference docs |

### Hallucination

| Symptom | Cause | Solution |
|---------|-------|----------|
| Made-up function names | Model guessing | Verify against documentation |
| Wrong API parameters | Model guessing | Check official docs |
| Fictional packages | Model guessing | Search npm/pypi before using |
| Incorrect syntax | Model confusion | Test the code immediately |

### Security Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| Hardcoded secrets | Model doesn't know about security | Add security rules to context |
| SQL injection | String concatenation | Specify parameterized queries |
| Missing input validation | Model focuses on happy path | Explicitly request validation |
| Insecure defaults | Model uses common patterns | Specify security requirements |

## Performance Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| Slow suggestions | Large context window | Reduce files in context |
| Timeouts | Network issues | Check connection, reduce request size |
| High memory usage | Too many files open | Close unused files |
| IDE lag | Extension conflict | Disable other AI extensions |

## Configuration Issues

### Rules Files Not Working

| Check | How |
|-------|-----|
| File location | Rules must be in project root or `.cursor/rules/` |
| File format | Use correct format for your tool |
| Syntax | Check for YAML/Markdown syntax errors |
| Restart | Some tools need restart to reload rules |
| Scope | Rules may only apply to certain file types |

### Context Not Found

| Check | How |
|-------|-----|
| File exists | Verify the file path is correct |
| File accessible | Check file permissions |
| File in scope | Some tools only see open files |
| Context limits | May exceed context window |

## Getting Better Output

### If Suggestions Are Bad

1. **Add more context** — Reference specific files
2. **Be more specific** — Exact requirements, not vague goals
3. **Show examples** — "Like this: [example]"
4. **Start new conversation** — Old context may be polluting
5. **Use rules files** — Persistent context across sessions

### If Output Is Wrong

1. **Share the error** — Paste exact error message
2. **Share the expected behavior** — What should happen
3. **Share related code** — Let AI see the full picture
4. **Ask for explanation** — Understand why it's wrong
5. **Try a different approach** — Rephrase the prompt

## Best Practices

- **Start simple** — Minimal context first, add as needed
- **Restart when stuck** — Fresh context often solves issues
- **Check tool updates** — Bugs are fixed in updates
- **Use official docs** — Tool-specific issues have official solutions
- **Ask in communities** — Other users have solved your problem

## Related Topics

- [AI Coding Assistants](ai-coding-assistants.md) — Tool-specific features
- [Context Engineering](context-engineering.md) — Improving suggestion quality
- [Limitations](ai-limitations.md) — What AI fundamentally gets wrong

## Further Learning

- [GitHub Copilot Troubleshooting](https://docs.github.com/en/copilot/troubleshooting-github-copilot) — Official troubleshooting
- [Cursor Troubleshooting](https://docs.cursor.com/troubleshooting) — Official troubleshooting

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
