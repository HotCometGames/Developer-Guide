# Project Management Troubleshooting

> Common project management problems, their root causes, and how to fix them.

> **Related:** [What Is Project Management?](what-is-project-management.md) | [Retrospectives](retrospectives.md) | [Sprint Execution](sprint-execution.md)

---

## How to Diagnose

Most project management problems are symptoms of deeper issues. Before jumping to solutions:

1. Is this a **people problem** or a **process problem**? (Process is easier to fix.)
2. Has this happened before? (Pattern suggests root cause.)
3. Does the team see it as a problem? (If not, your perception might be wrong.)

---

## Problem: Scope Creep

> Features keep getting added. The release never ships.

**Symptoms:**

- Stories appear mid-sprint without anything leaving
- The backlog grows faster than the team completes work
- Everyone is busy but nothing ships
- "We just need one more thing"

**Root causes:**

- No clear sprint goal or scope boundary
- Stakeholders bypass the backlog
- Product owner can't say no

**How to fix:**

1. **Enforce the sprint boundary** — Nothing enters a sprint without something of equal size leaving
2. **Make the PO the gatekeeper** — All requests go through the PO, who prioritizes against the backlog
3. **Use a "parking lot"** — Off-topic ideas go to a separate parking lot, not the sprint backlog
4. **Shape Up appetite** — Fixed time, variable scope. If it doesn't fit, cut scope.

## Problem: Missed Deadlines

> The team consistently ships late.

**Symptoms:**

- Sprint velocity is declining or unpredictable
- Stories are always "almost done" at sprint end
- Bug fixes take up more time than planned

**Root causes:**

- Overcommitment (team commits to more than they can deliver)
- Underestimation (unknowns not accounted for)
- Interruptions (support, meetings, unplanned work)

**How to fix:**

1. **Use yesterday's weather** — Commit to last sprint's velocity, not an average
2. **Add a buffer** — 20-30% capacity for unknowns
3. **Track interruption time** — Count support/meeting time and adjust capacity
4. **Swarm on blockers** — When a story is blocked, the team swarms to unblock

## Problem: Low Velocity

> The team seems to be working hard but produces less than expected.

**Symptoms:**

- Sprint after sprint of low points
- Stories are large and rarely finish
- Lots of context switching

**Root causes:**

- Technical debt is slowing the team down
- Too many work-in-progress items
- Unclear requirements (stories lack acceptance criteria)
- Team is demoralized or burned out

**How to fix:**

1. **Carve out tech debt sprints** — Dedicate a sprint to paying down debt
2. **Enforce WIP limits** — Even in Scrum, limit how many stories are "in progress"
3. **Improve story quality** — Invest in acceptance criteria before sprint planning
4. **Check team health** — Burnout, conflict, or low motivation. Fix the human layer first.

## Problem: Team Conflict

> People aren't collaborating well. Finger-pointing, silos, or avoidance.

**Symptoms:**

- Blame during retros
- People don't want to pair or work together
- Decisions get stuck because no one agrees
- Pull requests sit unreviewed

**Root causes:**

- Unclear roles and responsibilities
- Lack of psychological safety
- Personality conflicts (rare — usually a system problem)

**How to fix:**

1. **Clarify who owns what** — Document RACI or DACI for key decisions
2. **Create safe spaces** — Retros with the prime directive, anonymous feedback channels
3. **Use a facilitator** — If conflict is deep, bring in an external facilitator for a retro
4. **Team charter** — Write down working agreements: how do we handle disagreements?

## Problem: Stakeholder Pressure

> Leadership or clients keep demanding faster delivery or more features.

**Symptoms:**

- Team is asked to work overtime
- Quality is sacrificed for speed
- New requests come directly to developers, not the PO
- Roadmap changes weekly

**Root causes:**

- Lack of trust in the team's estimates
- No visibility into progress
- Stakeholders aren't involved in tradeoff decisions

**How to fix:**

1. **Show, don't tell** — Share burndown/burnup charts, velocity trends, and the board
2. **Present tradeoffs** — "We can ship X by March with these features, or Y with these features. Which do you prefer?"
3. **Protect the team** — The SM/PM buffers stakeholders so the team can focus
4. **Educate on agile** — Help stakeholders understand that changing scope changes the date

## Problem: Ceremony Fatigue

> The team is tired of meetings. Standups feel pointless. Planning drags.

**Symptoms:**

- People skip ceremonies
- Low energy in meetings
- "Can we just skip the retro and get back to work?"
- Planning takes 4 hours because stories aren't prepared

**Root causes:**

- Ceremonies have become check-the-box exercises
- No one sees value in them
- They run too long

**How to fix:**

1. **Tighten the timebox** — Standups: 15 min max. Retros: 45 min max.
2. **Cancel a ceremony** — Try skipping one retro and see if anything breaks
3. **Rotate formats** — Same retro format every sprint? Change it.
4. **Prepare** — PO should have backlog refined before planning. Developers should have questions before the meeting.

## Problem: Unclear Priorities

> Nobody knows what's most important. Everything is "high priority."

**Symptoms:**

- Team works on pet projects instead of backlog items
- Stakeholders are unhappy regardless of what ships
- Every request is marked P0/urgent/critical
- The backlog is unordered

**Root causes:**

- No product owner or weak product ownership
- No clear product vision or roadmap
- Everything genuinely is urgent (organizational dysfunction)

**How to fix:**

1. **Force ranking** — The backlog must be ordered. If everything is P0, nothing is.
2. **Use the Eisenhower Matrix** — Urgent vs Important. Only work on Important first.
3. **Define the "one thing"** — What's the single most important thing this sprint?
4. **Product vision** — Write down what the product is for. Use it to filter requests.

---

## Quick Reference

| Problem | Quick Fix | Systemic Fix |
|---------|-----------|--------------|
| Scope creep | Lock sprint scope | Enforce backlog → sprint boundary |
| Missed deadlines | Lower commitment next sprint | Track velocity, account for unknowns |
| Low velocity | Limit WIP, swarm | Pay down tech debt, fix stories |
| Team conflict | Facilitate a safe retro | Document roles, create working agreements |
| Stakeholder pressure | Share burndown charts | Present tradeoffs, protect team |
| Ceremony fatigue | Shorten or skip one | Rotate formats, prepare better |
| Unclear priorities | Rank the backlog | Define product vision, say no |

## Related Topics

- [Retrospectives](retrospectives.md) — The best place to surface and fix problems
- [Sprint Execution](sprint-execution.md) — Day-to-day execution patterns
- [Estimation & Planning](estimation-and-planning.md) — Better estimates reduce surprises

## Further Learning

- *The Phoenix Project* — Gene Kim (IT operations, but the patterns apply to all software)
- *Turn the Ship Around!* — David Marquet (leadership and team empowerment)
- *An Elegant Puzzle: Systems of Engineering Management* — Will Larson

---

> **Previous:** [Remote & Async Teams](remote-and-async-teams.md) | **Next:** [Testing](../12-testing/README.md)
