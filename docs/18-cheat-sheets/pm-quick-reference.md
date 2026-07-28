# Project Management Quick Reference

> One-page reference for Agile, Scrum, Kanban, sprints, and team ceremonies. Print this or bookmark it.

---

## Scrum Framework

| Ceremony | Duration | Purpose | Who |
|----------|----------|---------|-----|
| Sprint Planning | 2-4 hours | Define sprint goal, select backlog items | Entire team |
| Daily Standup | 15 min | Sync progress, surface blockers | Entire team |
| Sprint Review | 1-2 hours | Demo completed work, gather feedback | Team + stakeholders |
| Sprint Retrospective | 1-1.5 hours | Improve process, address issues | Entire team |

### Sprint Length

| Length | Best For |
|--------|----------|
| 1 week | Fast iteration, stable teams |
| 2 weeks | Most teams (recommended) |
| 3-4 weeks | Complex projects, large teams |

## User Stories

### Format

```
As a [user type],
I want [goal],
So that [benefit].
```

### INVEST Criteria

| Letter | Meaning | Check |
|--------|---------|-------|
| I | Independent | Can be developed alone? |
| N | Negotiable | Details can be discussed? |
| V | Valuable | Delivers value to user? |
| E | Estimable | Team can estimate effort? |
| S | Small | Fits in one sprint? |
| T | Testable | Has clear acceptance criteria? |

### Story Points (Fibonacci)

| Points | Meaning |
|--------|---------|
| 1 | Trivial, few hours |
| 2 | Small, half a day |
| 3 | Medium, 1 day |
| 5 | Large, 2-3 days |
| 8 | Very large, nearly a sprint |
| 13 | Epic, needs splitting |
| 21 | Too big, must decompose |

## Kanban

| Concept | Rule |
|---------|------|
| Visualize workflow | Board with columns: To Do, In Progress, Review, Done |
| Limit WIP | Max 2-3 items per person in progress |
| Manage flow | Aim for smooth, steady delivery |
| Make policies explicit | Clear definition of "done" for each column |
| Implement feedback loops | Regular reviews and retrospectives |
| Improve collaboratively | Team owns the process |

### WIP Limits

| Team Size | Recommended WIP |
|-----------|-----------------|
| 3 people | 5-6 total items |
| 5 people | 8-10 total items |
| 10 people | 15-20 total items |

## Definition of Done

| Criteria | Example |
|----------|---------|
| Code complete | Feature implemented per acceptance criteria |
| Tests pass | Unit, integration tests green |
| Code reviewed | At least one approval |
| Documentation updated | README, API docs if applicable |
| No critical bugs | QA sign-off |
| Deployed to staging | Verified in staging environment |
| Product owner accepted | Demo approved |

## Estimation Techniques

| Technique | How | When |
|-----------|-----|------|
| Planning poker | Team votes simultaneously | Sprint planning |
| T-shirt sizing | XS/S/M/L/XL classification | Backlog grooming |
| Timeboxing | Fixed time, variable scope | Hackathons, spikes |
| Three-point | Optimistic + Pessimistic + Most Likely / 3 | Complex tasks |
| Affinity mapping | Group similar items together | Large backlogs |

## Sprint Velocity

### Calculation

```
Velocity = Total story points completed / Number of sprints
```

### Usage

| Use | How |
|-----|-----|
| Capacity planning | Velocity × sprints in release = total capacity |
| Sprint commitment | Don't exceed average velocity |
| Forecasting | Points remaining / velocity = sprints needed |
| Improvement tracking | Velocity trends over time |

## Retrospective Formats

### Start / Stop / Continue

| Column | Question |
|--------|----------|
| Start | What should we start doing? |
| Stop | What should we stop doing? |
| Continue | What's working well and should continue? |

### 4Ls

| Column | Question |
|--------|----------|
| Liked | What did we enjoy? |
| Learned | What did we learn? |
| Lacked | What was missing? |
| Longed for | What did we wish we had? |

### Sailboat

| Area | Question |
|------|----------|
| Wind (good) | What's propelling us forward? |
| Anchor (bad) | What's slowing us down? |
| Rocks (risks) | What dangers lie ahead? |
| Island (goal) | Where are we headed? |

## Release Planning

| Step | Action |
|------|--------|
| 1 | Define release goal and timeline |
| 2 | Estimate total backlog size (story points) |
| 3 | Calculate velocity trend |
| 4 | Determine how many sprints needed |
| 5 | Identify MVP scope (minimum viable release) |
| 6 | Plan feature milestones per sprint |
| 7 | Identify dependencies and risks |
| 8 | Communicate plan to stakeholders |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Skipping retros | Team doesn't improve | Always hold retro, even if short |
| No sprint goal | Random work, no focus | Define a clear goal per sprint |
| Estimating in hours | Inaccurate, stressful | Use story points for relative sizing |
| Too many WIP items | Context switching, slow delivery | Limit WIP strictly |
| No definition of done | Inconsistent quality | Define and enforce DoD |
| Stakeholders bypass process | Chaos, unplanned work | All requests go through backlog |

---

> **Full section:** [Project Management](../11-project-management/README.md) | **Next:** [Developer Wisdom](wisdom-quick-reference.md)
