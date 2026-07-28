# Kanban

> A visual workflow management method that focuses on continuous delivery without overloading the team.

> **Related:** [Scrum](scrum.md) | [What Is Project Management?](what-is-project-management.md)

---

## What Is It?

Kanban is a **pull-based** system where work items flow through a visual board, and the team limits how many items can be in progress at once. Unlike Scrum, there are no sprints or fixed iterations — work is delivered continuously.

## The Core Principles

| Principle | Meaning |
|-----------|---------|
| **Visualize the workflow** | Make work visible on a board with columns |
| **Limit Work in Progress (WIP)** | Stop starting, start finishing |
| **Manage flow** | Focus on smooth, predictable delivery |
| **Make policies explicit** | Everyone knows the rules (e.g., Definition of Done per column) |
| **Implement feedback loops** | Review and improve the process regularly |
| **Improve collaboratively** | The team owns the system |

## The Kanban Board

```
┌────────────┬────────────┬───────────┬────────────┐
│   Backlog  │ In Progress│  Review   │    Done    │
│            │  (WIP: 3)  │ (WIP: 2)  │            │
├────────────┼────────────┼───────────┼────────────┤
│            │            │           │            │
│  Feature A │  Feature B │ Feature C │ Feature D  │
│            │            │           │            │
│  Feature E │            │           │ Feature F  │
│            │            │           │            │
│  Bug #123  │            │           │            │
│            │            │           │            │
└────────────┴────────────┴───────────┴────────────┘
```

Columns can be customized:

| Column | Purpose | Typical WIP Limit |
|--------|---------|-------------------|
| Backlog | Prioritized but not started | No limit |
| Analysis | Being understood/designed | 2 per person |
| In Progress | Being worked on | 1-2 per person |
| Review | Code review / QA | 2-3 per person |
| Done | Shipped | No limit |

## WIP Limits

WIP limits are the **heart of Kanban**. They force the team to finish work before starting new work.

| Team Size | Recommended Total WIP |
|-----------|---------------------|
| 3 people | 5-6 items |
| 5 people | 8-10 items |
| 10 people | 15-20 items |

**What happens when you hit a WIP limit?**
- No new work enters that column
- Someone must finish or pull back blocked items
- The team swarms on blockers

> **Tip:** If you hit WIP limits constantly, the limits are too high or the process is blocked. Fix the blockage rather than raising the limit.

## Flow Metrics

### Cycle Time

The time a work item takes to move from **started** to **finished**.

```
Cycle Time = Date Done - Date Started
```

| Cycle Time | Team Health |
|------------|-------------|
| 1-3 days | Healthy, fast flow |
| 1-2 weeks | Normal for larger features |
| 1+ months | Too much work-in-progress or blockers |

### Lead Time

The time from **when work is requested** to **when it's finished**.

```
Lead Time = Date Done - Date Requested
```

Lead time includes time spent sitting in the backlog. Cycle time does not.

### Cumulative Flow Diagram (CFD)

```mermaid
graph LR
    A[Backlog] --> B[In Progress]
    B --> C[Review]
    C --> D[Done]

    note on A: "Area between lines = WIP"
```

A CFD shows the number of items in each state over time. It helps you spot:

- **Growing backlog** — Pulling in more work than finishing
- **Widening WIP band** — Too many items in progress
- **Flat done line** — Nothing is shipping

## Kanban vs Scrum

| Dimension | Scrum | Kanban |
|-----------|-------|--------|
| Cadence | Fixed sprints (1-4 weeks) | Continuous flow |
| Roles | PO, SM, Developers | No prescribed roles |
| Ceremonies | Planning, standup, review, retro | None required (add as needed) |
| Metrics | Velocity | Cycle time, lead time, throughput |
| WIP limits | Implicit (sprint scope) | Explicit (per column) |
| Best for | Feature development | Support, maintenance, ops |
| Change model | Batch delivery per sprint | Continuous delivery |

## When to Use Kanban

| Use Kanban When | Use Scrum When |
|----------------|---------------|
| Work is unpredictable (bugs, support) | Work can be planned in advance |
| Priorities change frequently | Priorities are stable for 2 weeks |
| Team is small and self-managing | Team needs structured ceremonies |
| You want to reduce cycle time | You want predictable delivery cadence |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| No WIP limits | Everything is "in progress", nothing finishes | Set explicit limits, enforce them |
| Too high WIP limits | Limits don't constrain behavior | Lower limits until they force behavior change |
| One-piece flow for everything | Blocking an item blocks everything | Allow exceptions for urgent fixes |
| No policies | Vague "done" means different things per person | Write the rules for each column |
| Ignoring cycle time | Can't improve what you don't measure | Track cycle time, review trends |

## Related Topics

- [Scrum](scrum.md) — The iterative counterpart to Kanban's flow
- [Estimation & Planning](estimation-and-planning.md) — Kanban uses flow metrics instead of velocity
- [Sprint Execution](sprint-execution.md) — Standups work for Kanban teams too

## Further Learning

- *Kanban: Successful Evolutionary Change for Your Technology Business* — David J. Anderson
- *Lean from the Trenches* — Henrik Kniberg

---

> **Next:** [User Stories](user-stories.md) | **Previous:** [Scrum](scrum.md)
