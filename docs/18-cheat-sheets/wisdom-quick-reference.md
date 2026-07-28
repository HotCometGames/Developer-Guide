# Developer Wisdom Quick Reference

> One-page reference for engineering principles, code smells, refactoring techniques, and career advice. Print this or bookmark it.

---

## Core Principles

### KISS — Keep It Simple, Stupid

| Instead of | Do |
|------------|-----|
| Clever one-liner | Readable multi-line code |
| Complex abstraction | Simple solution that works |
| Premature optimization | Clean code, optimize later |

### YAGNI — You Aren't Gonna Need It

| Instead of | Do |
|------------|-----|
| Building for "maybe someday" | Build for now |
| Extra features "just in case" | Only what's required |
| Generic framework | Specific solution |

### DRY — Don't Repeat Yourself

| Instead of | Do |
|------------|-----|
| Copy-paste code | Extract function or module |
| Duplicated logic | Shared utility |
| Repeated config | Single source of truth |

### SoC — Separation of Concerns

| Instead of | Do |
|------------|-----|
| God function | Functions with one job |
| Mixed concerns (DB + UI) | Layered architecture |
| Monolithic config | Separate configs per concern |

## Code Smells

| Smell | What It Looks Like | Refactoring |
|-------|--------------------|-------------|
| Long method | 100+ lines | Extract Method |
| God class | One class does everything | Split by Responsibility |
| Duplicated code | Same logic in 3+ places | Extract Function/Module |
| Long parameter list | 5+ parameters | Introduce Parameter Object |
| Primitive obsession | Using strings for everything | Introduce Value Object |
| Feature envy | Method uses another class's data | Move Method |
| Data clumps | Same 3 variables together | Extract Class |
| Switch statements | Long if/else or switch | Replace with Polymorphism |
| Speculative generality | Unused abstractions | Delete it |
| Dead code | Commented/unreachable code | Delete it |

## Refactoring Techniques

### Small Steps

| Technique | When | How |
|-----------|------|-----|
| Extract Method | Long function | Pull code into named function |
| Rename | Unclear naming | Change name to be descriptive |
| Inline | Unnecessary indirection | Replace call with body |
| Move Method | Wrong location | Move to correct class/module |
| Extract Class | Mixed responsibilities | Split into two classes |
| Replace Temp with Query | Temporary variable | Convert to function call |
| Introduce Explaining Variable | Complex condition | Name the condition |
| Decompose Conditional | Complex if/else | Extract conditions into functions |

### Before Refactoring

1. **Ensure tests exist** — refactor with confidence
2. **Make small changes** — one refactoring at a time
3. **Commit frequently** — easy to revert
4. **Run tests after each change** — catch regressions early
5. **Don't mix refactoring with features** — separate commits

## Learning Strategies

### The 70-20-10 Model

| Source | % | How |
|--------|---|-----|
| Experience | 70% | Build projects, solve problems |
| Others | 20% | Code reviews, pair programming, mentoring |
| Formal | 10% | Courses, books, documentation |

### Deliberate Practice

| Step | Action |
|------|--------|
| 1 | Choose a specific skill to improve |
| 2 | Work at the edge of your ability |
| 3 | Get immediate feedback |
| 4 | Repeat with reflection |
| 5 | Focus on weaknesses, not strengths |

### Spaced Repetition for Code

| Interval | Review |
|----------|--------|
| Day 1 | Learn concept |
| Day 3 | Review notes |
| Day 7 | Practice exercise |
| Day 14 | Build small project |
| Day 30 | Teach someone else |

## Debugging Mental Model

```
1. Reproduce the bug
2. Understand the expected behavior
3. Understand the actual behavior
4. Narrow down the scope
5. Form hypothesis
6. Test hypothesis
7. Fix the root cause
8. Add test to prevent regression
```

### Debugging Checklist

- [ ] Can you reproduce it consistently?
- [ ] What changed recently?
- [ ] Is it in your code or a dependency?
- [ ] What do the logs say?
- [ ] Is it a data issue?
- [ ] Is it a timing/concurrency issue?
- [ ] Is it environment-specific?

## Career Advice

### Skill Growth

| Level | Focus | How |
|-------|-------|-----|
| Junior | Syntax, tools, basics | Build things, follow tutorials |
| Mid | Patterns, architecture, trade-offs | Read code, contribute to OSS |
| Senior | System design, mentoring, strategy | Lead projects, write RFCs |
| Staff+ | Org impact, technical vision | Cross-team initiatives, ADRs |

### High-Leverage Activities

| Activity | Impact |
|----------|--------|
| Writing clear documentation | Saves hours for everyone |
| Automated testing | Prevents regressions, enables refactoring |
| Code reviews | Knowledge sharing, quality improvement |
| Mentoring | Multiplies team capability |
| Removing blockers | Unblocks entire team |

### Burnout Prevention

| Signal | Action |
|--------|--------|
| Dreading Monday | Set boundaries, talk to manager |
| Can't stop thinking about work | Schedule hard stop, disconnect |
| Cynical about everything | Take vacation, seek support |
| Physical exhaustion | Prioritize sleep, exercise |
| No joy in coding | Work on side projects, learn new tech |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Gold plating | Over-engineering | Ship minimum, iterate |
| Resume-driven development | Wrong tech choices | Choose boring technology |
| Not reading error messages | Wasted time | Read the full error first |
| Copy-pasting from Stack Overflow | Introduces bugs | Understand before adapting |
| Ignoring failing tests | Reduces test value | Fix or remove broken tests |
| Not asking for help | Stuck for hours | Timebox, then ask |

## Mental Models

| Model | Application |
|-------|-------------|
| First Principles | Break problem to fundamentals |
| Inversion | Think about what to avoid |
| 80/20 Rule | Focus on highest impact |
| Second-order effects | Consider consequences of consequences |
| Map is not the territory | Model ≠ reality |
| Margin of Safety | Build in buffer for unknowns |

---

> **Full section:** [Developer Wisdom](../17-developer-wisdom/README.md) | **Next:** [Cheat Sheets Overview](terminal-quick-reference.md)
