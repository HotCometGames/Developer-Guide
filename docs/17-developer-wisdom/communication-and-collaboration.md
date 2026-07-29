# Communication & Collaboration

> Writing, reviewing, mentoring, and working effectively with other engineers.

> **Related:** [Decision Making & Trade-offs](decision-making-and-tradeoffs.md) | [Debugging Mindset](debugging-mindset.md)

---

## What Is It?

Software engineering is a team sport. The best code in the world is worthless if no one can understand, maintain, or build on it.

## Code Review

### For the Author

| Principle | Why |
|-----------|-----|
| Keep PRs small | < 400 lines is easier to review thoroughly |
| Write a clear description | What does this PR do? Why? What's the approach? |
| Self-review first | Catch your own nits before asking others |
| Respond to comments | Address every comment — fix, explain, or discuss |
| Separate refactoring from features | Logic changes are hard to see in a sea of renames |

### For the Reviewer

| Principle | Why |
|-----------|-----|
| Review the diff, not the author | Focus on code quality, not who wrote it |
| Ask questions, don't dictate | "What's the reasoning for this approach?" vs "This is wrong" |
| Distinguish nits from blockers | Prefix with "nit:" for style suggestions |
| Approve quickly when it's ready | Don't hold PRs hostage for minor preferences |
| Explain your reasoning | "This approach is fragile because..." is better than "Do it differently" |

### What to Look For

```
□ Does the code solve the problem?
□ Are there edge cases or error paths missing?
□ Is the naming clear?
□ Are there tests for the new code?
□ Is there unnecessary complexity?
□ Does it follow the project's conventions?
```

## Writing Documentation

Good documentation answers the reader's question before they ask it:

| Question | Where It Belongs |
|----------|-----------------|
| What does this project do? | README |
| How do I set it up? | README or CONTRIBUTING.md |
| How do I use this API? | Docstrings, module docs |
| Why was this decision made? | ADR (Architecture Decision Record) |
| What do I need to know before deploying? | Deployment guide |

### Docstring Patterns

```python
def calculate_discount(price: float, rate: float) -> float:
    """Calculate discounted price.

    Args:
        price: Original price before discount.
        rate: Discount rate as decimal (0.1 = 10%).

    Returns:
        Discounted price.

    Raises:
        ValueError: If price or rate is negative.
    """
```

## Mentoring

| Approach | What It Looks Like |
|----------|--------------------|
| Show and explain | Walk through code together, explain the reasoning |
| Guided practice | "I'll watch — you write the solution" |
| Review and discuss | Review their PR, discuss trade-offs |
| Reverse mentoring | Learn from their fresh perspective |

## Giving Feedback

| Situation | Good Approach |
|-----------|---------------|
| Code quality issue | "This works, but here's a more maintainable approach..." |
| Missed requirement | "Did we consider the case where..." |
| Technical disagreement | "I see it differently. Here's my reasoning — what am I missing?" |
| Pattern repeated across PRs | "I've noticed a pattern in your recent PRs. Can we talk through it?" |

## Asking for Help

| Instead of | Try |
|------------|-----|
| "Can you fix this?" | "I'm stuck on X. I tried A, B, and C. Can you point me in the right direction?" |
| Not asking for an hour | Timebox: 15-30 minutes of research, then ask |
| DMing someone without context | Provide the problem, what you've tried, and links |

## Best Practices

- **Over-communicate context** — async communication loses tone and nuance
- **Prefer written communication** — it's searchable, referenceable, and inclusive of time zones
- **Assume good intent** — most "bad" code comes from constraints or knowledge gaps, not malice
- **Celebrate wins publicly** — praise in public, feedback in private
- **Document decisions** — if a discussion takes more than 5 minutes, write down the conclusion

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Writing too many comments | Noise, maintenance burden | Comments explain WHY, code shows HOW |
| Approving PRs without understanding | Merged bugs, tech debt | Take the time to understand the diff |
| Giving vague feedback | "This could be better" | Be specific: "This function does two things — split it" |
| Not documenting decisions | Same discussion next month | Write ADRs for significant decisions |
| Waiting for perfect code | Nothing ships | Good code ships. Perfect code is theoretical. |

## What's Next?

Apply these skills with solid [Engineering Principles](engineering-principles.md) to make your code easier to review and maintain.
