# AI Workflows

> End-to-end workflows for common development tasks using AI assistance. Feature development, refactoring, documentation, and prototyping.

---

## What Is It?

AI workflows are structured, step-by-step processes that combine prompting, context engineering, and tool usage to accomplish development tasks efficiently. Instead of ad-hoc prompting, you follow proven patterns.

> **Related:** [Prompt Engineering](prompt-engineering.md) for prompt techniques. [Context Engineering](context-engineering.md) for managing context. [AI Agents](ai-agents.md) for autonomous execution.

---

## Why Does It Matter?

| Ad-Hoc Prompting | Structured Workflows |
|------------------|---------------------|
| Random results | Consistent, reliable output |
| Miss steps | Complete coverage |
| Waste time re-explaining | Context carries forward |
| Inconsistent quality | Repeatable process |

## Feature Development Workflow

### The Flow

```
1. Spec → 2. Plan → 3. Implement → 4. Test → 5. Review → 6. Ship
```

### Step 1: Spec to AI

```
I need to build a [feature]. Here's the requirement:
[User story or description]

Tech stack: [your stack]
Existing patterns: [reference files]

Help me break this into implementation steps.
```

### Step 2: Plan with AI

```
Based on the steps above:
1. What files need to be created or modified?
2. What's the order of implementation?
3. What are the risks or edge cases?
4. What tests should I write?
```

### Step 3: Implement

```
Let's implement step 1: [specific task]

Follow the pattern in [existing file].
Use [specific libraries/patterns].
Handle [edge cases].
```

### Step 4: Test

```
Write tests for the code we just implemented.
Cover:
- Happy path
- Edge cases: [list them]
- Error handling
- Integration with [related component]
```

### Step 5: Review

```
Review everything we've built:
[paste all changed files]

Check for:
1. Bugs and logic errors
2. Security issues
3. Performance concerns
4. Code style consistency
```

### Step 6: Ship

```
Help me write a PR description for these changes:

[paste git diff or file list]

Include:
- What changed and why
- Breaking changes
- Test coverage
- Deployment notes
```

## Refactoring Workflow

### The Flow

```
1. Understand → 2. Plan → 3. Execute → 4. Verify → 5. Clean up
```

### Step 1: Understand

```
I need to refactor [file/module] to [goal].

Here's the current code:
[paste code]

What does it do currently? What are the dependencies?
```

### Step 2: Plan

```
Create a refactoring plan:
1. What changes are needed?
2. What's the order to avoid breaking things?
3. What tests exist to verify behavior is preserved?
4. What's the risk level?
```

### Step 3: Execute

```
Execute step 1 of the refactoring plan:
[specific change]

Show me the diff, don't just show the final code.
```

### Step 4: Verify

```
The refactoring is done. Help me verify:
1. Run existing tests
2. Check for any behavioral changes
3. Verify performance hasn't degraded
```

### Step 5: Clean up

```
The refactoring works. Help me:
1. Update any related documentation
2. Remove dead code
3. Improve variable/function names if needed
```

## Documentation Workflow

### The Flow

```
1. Code exists → 2. AI generates docs → 3. Review → 4. Polish
```

### Generate API Docs

```
Generate documentation for this API module:

[paste module]

Include:
- Function signatures with types
- Parameter descriptions
- Return value descriptions
- Usage examples
- Error cases
```

### Generate README

```
Write a README for this project:

[paste package.json or pyproject.toml]
[paste directory structure]

Include:
- What the project does
- Quick start guide
- Configuration options
- API reference
- Contributing guidelines
```

### Generate Inline Docs

```
Add JSDoc/docstring comments to this code:

[paste code]

Follow [Google/NumPy/Sphinx] docstring style.
Include parameter types, return types, and examples.
```

## Prototyping Workflow

### The Flow

```
1. Idea → 2. Minimal spec → 3. Quick implement → 4. Test manually → 5. Decide
```

### Step 1: Idea to Spec

```
I have an idea for [brief description].

Help me create a minimal spec:
- Core functionality (must have)
- Nice-to-have features
- Technical approach
- Estimated complexity
```

### Step 2: Quick Implement

```
Build the MVP: [specific feature]

Keep it simple:
- Minimal error handling
- Basic UI (if applicable)
- Hardcoded config is fine
- Focus on core logic
```

### Step 3: Manual Test

```
I tested the prototype. Here's what happened:
[describe results]

What works? What doesn't? Should I continue or pivot?
```

## Legacy Code Workflow

### The Flow

```
1. Understand → 2. Document → 3. Test → 4. Modernize → 5. Verify
```

### Step 1: Understand

```
I inherited this codebase. Help me understand:

[paste key files]

What does it do? What's the architecture? What are the risks?
```

### Step 2: Document

```
Create documentation for this legacy module:

[paste code]

Include:
- What it does
- How it connects to other modules
- Known issues
- Data flow
```

### Step 3: Test Before Changing

```
Write tests for this legacy code BEFORE we modify it:

[paste code]

These tests should verify current behavior so we know if we break anything.
```

### Step 4: Modernize

```
Now let's modernize this code:
[paste legacy code]

Goals:
- [Specific modernization goal]
- Maintain backward compatibility
- Follow existing patterns in [modern file]
```

## Best Practices

- **Follow the workflow** — Don't skip steps, even when it feels fast to do so
- **One step at a time** — Don't ask for everything in one prompt
- **Verify at each step** — Run tests, check output, review before moving on
- **Keep context fresh** — Start new conversations for new major steps
- **Document decisions** — Write down why you chose certain approaches

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Skipping the spec | Build the wrong thing | Define what you want first |
| Asking for everything at once | Incomplete, low quality output | Break into steps |
| Not verifying intermediate steps | Errors compound | Test after each step |
| Mixing concerns in one chat | Confused context | Start new conversation per major step |
| Not reviewing diffs | Subtle issues slip through | Review every change |

## Related Topics

- [Prompt Engineering](prompt-engineering.md) — Better prompts for each step
- [Context Engineering](context-engineering.md) — Managing what AI sees
- [AI Agents](ai-agents.md) — Autonomous execution of workflows

## Further Learning

- [AI-Assisted Development Patterns](https://www.oreilly.com/library/view/ai-assisted-software/9781098153113/) — Enterprise patterns
- [GitHub Copilot Best Practices](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot) — Official guide

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
