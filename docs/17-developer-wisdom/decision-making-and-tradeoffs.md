# Decision Making & Trade-offs

> Making good engineering choices when there's no perfect answer.

> **Related:** [Engineering Principles](engineering-principles.md) | [Learning & Growth](learning-and-growth.md) | [Communication & Collaboration](communication-and-collaboration.md)

---

## What Is It?

Engineering is the art of making decisions under constraints. Every choice involves trade-offs — time vs quality, flexibility vs simplicity, speed vs correctness.

## Mental Models

Mental models are thinking tools that help you analyze problems from different angles.

### First Principles

Break a problem down to its fundamentals, then rebuild from there:

```
Conventional thinking:  "We need a database, so let's use Postgres"
First principles:       "We need to store and query user data with <100ms latency. What options exist?"
                        → Could be Postgres, SQLite, a file, or even an in-memory cache
```

| Instead of | Try |
|------------|-----|
| "That's how we've always done it" | "What are the actual requirements?" |
| "Everyone uses X" | "Does X solve our specific problem?" |
| "Copy the existing system" | "Design for what we need, not what we had" |

### Inversion

Think about what you want to avoid, then avoid those things:

```
Forward:  "How do we make this system reliable?"
Inverse:  "What would make this system unreliable?"
          → Network failures, data corruption, config errors
          → Now work backward: add retries, validation, checksums
```

### 80/20 Rule (Pareto Principle)

80% of the value comes from 20% of the effort:

| Effort | Impact | Example |
|--------|--------|---------|
| First 20% | 80% of value | Core CRUD, main user path |
| Next 30% | 15% of value | Edge cases, nicer UI |
| Last 50% | 5% of value | Perfect error messages, 100% code coverage |

Ship the first 20%, iterate from feedback.

### Opportunity Cost

Every hour spent on X is an hour not spent on Y:

```
Time spent:    Perfecting the build pipeline (3 days)
Could have:    Shipped 3 features that users are waiting for
```

The best decision isn't just "is X good?" — it's "is X better than everything else we could do with this time?"

## Choosing Technologies

| Factor | Questions |
|--------|-----------|
| Maturity | Has this been used in production at scale? |
| Community | Can I find answers, packages, and contributors? |
| Learning curve | How long until the team is productive? |
| Exit cost | How hard is it to switch away from this? |
| Team fit | Does anyone want to maintain this? |

### Consensus on Boring Technology

> "Choose boring technology" — Dan McKinley

A "boring" technology is one you know well, has predictable behavior, and has been proven at scale. It's not flashy, but it won't surprise you at 3 AM.

| Boring (Good) | Exciting (Risky) |
|---------------|-------------------|
| Postgres, SQLite | New NoSQL database with 500 GitHub stars |
| Python, TypeScript | Language released last month |
| Linux, Docker | New orchestrator built by a startup |

## Saying No

Good engineering requires saying no to bad ideas, premature complexity, and scope creep.

| Instead of | Say |
|------------|-----|
| "Sure, we can add that this sprint" | "What would we drop to fit that in?" |
| "Let's use microservices" | "Let's start with a monolith and split when we understand the boundaries" |
| "We should rewrite this" | "What are the top 3 problems with the current system?" |

## Best Practices

- **Write down the decision** — ADR (Architecture Decision Record) captures context and rationale
- **State assumptions explicitly** — "We assume < 1000 requests/second" — when that changes, revisit
- **Prefer reversible decisions** — if you can undo it, move fast. If it's hard to undo, move carefully
- **Set a decision deadline** — more time doesn't always mean better decisions
- **Escalate when blocked** — if you can't decide, get more data or push the decision up

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Analysis paralysis | Never making a decision | Set a deadline, make the best call with available data |
| Confirmation bias | Only considering evidence that supports your preference | Seek out counterarguments |
| Status quo bias | Sticking with what's familiar | Evaluate options as if starting from scratch |
| Sunk cost fallacy | Continuing because you've already invested | Past investment is irrelevant to future decisions |
| First idea bias | Going with the first option that comes to mind | Generate at least 3 alternatives before picking one |

## What's Next?

Good decisions are easier with good [Communication & Collaboration](communication-and-collaboration.md) to get input from the right people.
