# Architecture Decision Records

> A lightweight way to capture architectural decisions — why they were made, what alternatives were considered, and what the consequences are.

> **Related:** [What Is Software Architecture?](what-is-software-architecture.md) | [Architecture Styles](architecture-styles.md)

---

## What Is It?

An Architecture Decision Record (ADR) is a **short document** that captures a significant architectural decision. Think of it as a commit message for your architecture — it tells future you (and your team) **why** something was done a certain way.

## Why Does It Exist?

Without ADRs, every project eventually encounters:

- **Lost context** — "Why did we choose MongoDB over Postgres?" No one remembers.
- **Repeated debates** — The same decision gets argued every 6 months.
- **Fear of change** — No one knows why something was designed a certain way, so no one dares change it.
- **Onboarding drag** — New team members have no idea why things are the way they are.

ADRs solve this by writing down the decision **when it's made**, while the context is fresh.

## Mental Model

```
Code change records WHAT changed (git commit).
ADRs record WHY it changed that way.
```

An ADR is like a **git commit message for architecture**.

## The ADR Format

A good ADR fits on one page. Use this template:

```markdown
# ADR-NNN: Title

## Status
[Proposed | Accepted | Deprecated | Superseded]

## Context
What is the situation that requires a decision?
What forces are at play? (technical, business, timeline, team)

## Decision
What did we decide to do?

## Consequences
### Positive
- What becomes easier?

### Negative
- What becomes harder or more risky?

### Neutral
- What else changes?

## Alternatives Considered (Optional)
- Option A — why not chosen
- Option B — why not chosen
```

### Full Example

```markdown
# ADR-001: Use PostgreSQL as Primary Database

## Status
Accepted

## Context
We are building a financial reporting system that requires:
- ACID compliance for transaction integrity
- Complex reporting queries across multiple dimensions
- Strong data integrity guarantees (no silent corruption)

The team has experience with both PostgreSQL and MongoDB.

## Decision
We will use PostgreSQL as our primary database.

## Consequences
### Positive
- ACID compliance guarantees transaction safety
- Rich query capabilities (window functions, CTEs, JSONB)
- Mature ecosystem with excellent tooling
- Strong community and documentation

### Negative
- Schema changes require migrations (more overhead than schemaless)
- Horizontal scaling is harder than MongoDB (need read replicas, sharding)
- JSONB is less flexible than MongoDB's native document model

### Neutral
- Will need to implement read replicas for reporting queries
- Will need to manage connection pooling

## Alternatives Considered
- **MongoDB**: Rejected because we need ACID transactions across
  multiple documents, which MongoDB supports poorly compared to Postgres.
- **SQLite**: Rejected because we need concurrent write access from
  multiple application instances.
```

## When to Write an ADR

Write an ADR when:

- **A decision has significant consequences** — changing databases, adopting a new pattern, choosing an architecture style
- **The decision is hard to undo** — infrastructure choices, framework decisions
- **The team debated it** — if it took more than 10 minutes to decide, write it down
- **A newcomer might question it** — if the answer isn't obvious, document it

> **Tip:** Not every decision needs an ADR. "We'll use pytest instead of unittest" probably doesn't warrant one. "We'll adopt event sourcing for the order service" definitely does.

## ADR Lifecycle

```mermaid
graph LR
    P[Proposed] -->|Reviewed| A[Accepted]
    A -->|No longer relevant| D[Deprecated]
    D -->|Replaced by| S[Superseded]
    A -->|New decision overrides| S
```

## Storing ADRs

Keep ADRs in the repository alongside the code:

```
docs/
└── adr/
    ├── ADR-001-use-postgresql.md
    ├── ADR-002-adopt-cqrs.md
    ├── ADR-003-microservices-boundaries.md
    └── index.md
```

## When ADRs Pay Off Most

| Scenario | Impact |
|----------|--------|
| Team turnover | New members ramp up 10x faster |
| Long-lived projects | Decisions from 3 years ago still make sense |
| Distributed teams | Async decision-making with written context |
| Compliance / audits | Evidence of why decisions were made |
| Post-mortems | Trace what decisions led to the outage |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Too many ADRs | Nobody reads them | Only write for significant decisions |
| Too long | Nobody reads them | Keep to one page |
| Writing after the fact | Context is lost, rationalization | Write during or immediately after the decision |
| Not updating status | ADR shows "Accepted" but decision was reversed | Update the status, add superseding ADR |
| Storing outside the repo | Versioning isn't tied to code | Store ADRs in the codebase |

## Related Topics

- [What Is Software Architecture?](what-is-software-architecture.md) — Why architecture decisions matter
- [Architecture Styles](architecture-styles.md) — Common topics for ADRs

## Further Learning

- [Documenting Architecture Decisions — Michael Nygard](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) — The original ADR article
- [ADR GitHub organization](https://adr.github.io/) — Tools, templates, resources

---

> **Next:** [Scalability Patterns](scalability-patterns.md) | **Previous:** [Dependency Injection](dependency-injection.md)
