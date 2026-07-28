# Sprint Execution

> The day-to-day of running a sprint — standups, tracking, adjustments, and getting work across the finish line.

> **Related:** [Scrum](scrum.md) | [Estimation & Planning](estimation-and-planning.md) | [Retrospectives](retrospectives.md)

---

## What Is It?

Sprint execution is the **practice of running a sprint day-to-day** — keeping work visible, resolving blockers quickly, and making small adjustments without losing sight of the sprint goal.

## The Sprint Structure

### Day 1: Sprint Planning

- Define the sprint goal
- Select stories from the backlog
- Break stories into tasks (optional — some teams skip this)
- **Commitment:** The team agrees on a sprint scope

### Days 2-N: Daily Work + Standups

- Team works on assigned stories
- Daily standup for coordination
- Stories move across the board: To Do → In Progress → Review → Done

### Last Day: Sprint Review + Retrospective

- Demo completed work to stakeholders
- Sprint retrospective for the team

## Daily Standups

### Format

Everyone answers three questions in 60 seconds or less:

| Question | Purpose |
|----------|---------|
| What did I do yesterday? | Quick progress check |
| What will I do today? | Commitment for the next 24 hours |
| What's blocking me? | Surface issues immediately |

### Don'ts

| ❌ Don't | ✅ Do |
|----------|------|
| Read from a script | Speak naturally |
| Solve problems in the meeting | Take blockers offline |
| Make it a status report to the manager | Use it for team coordination |
| Let it run over 15 minutes | Park deep discussions for after |

> **Tip:** Try walking the board instead of going person-by-person. Start at "Done" and work backward to "To Do" — it focuses on the work, not the people.

## Tracking Progress

### Burndown Chart

Shows remaining work vs. time remaining.

```
Points Remaining
  ^
30 | *  (start of sprint, 30 points)
  |   \
25 |    \
  |     \
20 |      *
  |       \
15 |        *  (ideal line: points decreasing evenly)
  |         \
10 |          *
  |           \
 5 |            *
  |             \
 0 +------------------------> Days
   1  2  3  4  5  6  7  8  9 10
```

| Pattern | Meaning | Action |
|---------|---------|--------|
| Cliff drop day 1 | Task splitting, not tracking | Track at story level |
| Burn up (going up) | Scope was added mid-sprint | Stop — PO shouldn't add scope |
| Flat then steep | Blockers early, rushed delivery at end | Surface blockers faster |
| Above ideal line | Behind schedule | Cut scope, swarm, or accept |
| Below ideal line | Ahead of schedule | Don't add scope. Breathe. |

### Burnup Chart

Shows work completed vs. total scope. Better for communicating with stakeholders because it clearly shows scope changes.

```
Completed
  ^
40 |    Total scope (increases when stories added)
  |   /\
30 |  /  \
  | /    \
20 |/      \  (completed work)
  |       \
10 |        \
  |         \
 0 +------------------------> Time
```

## Handling Interruptions

| Interruption | How to Handle |
|-------------|---------------|
| Urgent bug | If small (1 hour), fix it. If larger, the PO decides: pull a story or abort |
| Stakeholder request | "Add it to the backlog — we'll prioritize next sprint" |
| Team member out sick | Swarm on remaining work, reduce scope |
| Technical blocker | Timebox investigation. If stuck, escalate. |

> **Rule:** Nothing enters the sprint after planning without something of equal size leaving.

## Swarming

When a story is blocked or behind, the team **swarms** — multiple people work on the same story rather than starting new ones.

```
Bad:    Person A: Story 1 (almost done)
        Person B: Story 2 (just started)
        Person C: Story 3 (just started)

Good:   Person A: Story 1 (lead)
        Person B: Story 1 (helping test)
        Person C: Story 1 (helping review)
```

> **Tip:** Start together, finish together. Swarming ensures you finish some stories completely rather than all stories partially.

## The Sprint Goal

Every sprint should have **one goal** that ties the selected stories together.

| Good Sprint Goals | Bad Sprint Goals |
|------------------|-----------------|
| "Implement user onboarding flow" | "Complete 25 story points" |
| "Enable social login" | "Work through the backlog" |
| "Fix top 5 performance issues" | "Keep working on features" |

The sprint goal helps the team make tradeoffs: "This new request doesn't align with our goal — it can wait."

## When Things Go Wrong

| Problem | Response |
|---------|----------|
| Story is more complex than expected | Swarm. If still blocked, PO may cut scope |
| Team member is out | Reassign unfinished work. Don't overload others |
| External blocker | SM escalates. Consider aborting the sprint (rare) |
| Sprint goal no longer relevant | Cancel the sprint. Replan. This is not failure. |
| Scope keeps creeping | "Not this sprint. Add it to the backlog." |

> **Note:** It's better to **cancel a sprint** and replan than to spend two weeks on work that no longer matters. Sprints are containers, not prisons.

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| No sprint goal | Random assortment of work | Define one clear goal |
| Standups as status reports | 30 minutes, no value | Keep to 15 minutes, focus on blockers |
| Adding scope mid-sprint | Nothing finishes | Not without removing equal scope |
| Ignoring the board | Tracking in people's heads | Make the board the source of truth |
| Hero culture | Burnout, bus factor | Swarm, don't let one person carry the sprint |
| No end-of-sprint cleanup | Stale stories, inaccurate board | Clean up before review |

## Related Topics

- [Scrum](scrum.md) — The framework that defines sprint structure
- [Retrospectives](retrospectives.md) — How to improve sprint execution
- [Kanban](kanban.md) — Continuous flow alternative to sprints

## Further Learning

- *Scrum: The Art of Doing Twice the Work in Half the Time* — Jeff Sutherland
- *Sprint* — Jake Knapp (for design sprints, a different but related concept)

---

> **Next:** [Retrospectives](retrospectives.md) | **Previous:** [Estimation & Planning](estimation-and-planning.md)
