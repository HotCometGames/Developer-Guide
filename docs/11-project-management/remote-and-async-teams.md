# Remote & Async Teams

> How to build, run, and sustain a software team that isn't in the same room — and doesn't need to be.

> **Related:** [Sprint Execution](sprint-execution.md) | [Retrospectives](retrospectives.md) | [Scrum](scrum.md)

---

## What Is It?

Remote and async work is the practice of **collaborating across time zones and locations** without requiring everyone to be online at the same time. Async-first means you optimize for communication that doesn't require an immediate response.

## The Core Shift

| In-Person | Remote-First |
|-----------|-------------|
| "I'll ask them at their desk" | "I'll write it in the shared doc" |
| Meeting to share information | Document then discuss |
| Decisions in a room | Decisions in a thread |
| Work happens 9-5 | Work happens when productive |
| Visibility = being seen | Visibility = written updates |
| Hallway conversations | Public channels (no DMs for decisions) |

## The Two Enemies of Remote Work

### 1. Too Many Synchronous Meetings

| Problem | Fix |
|---------|-----|
| 4 hours of standups, planning, review, retro per week | Keep ceremonies. Cut everything else. |
| "Quick sync" calls that replace written communication | "Write it down first. We'll meet if the doc is unclear." |
| All-hands meetings that could be a video | Record updates, async Q&A |
| Meeting to decide something that could be a poll | Slack poll + 24-hour deadline |

### 2. Async Gaps

| Problem | Fix |
|---------|-----|
| 12-hour response time blocks progress | Set expectations: "24-hour response is normal" |
| Missing context because you weren't in the meeting | Record everything, share notes publicly |
| Decisions made in DMs that affect the team | Public channels for project decisions |
| New hire doesn't know the history | Maintain a team wiki, ADRs, decision logs |

## The Async-First Communication Stack

| Layer | Tool | When |
|-------|------|------|
| **Permanent docs** | Wiki, Notion, GitHub Wiki | Decisions, guides, onboarding |
| **Async discussion** | Slack, Teams, Discourse | Questions, updates, lightweight discussion |
| **Project tracking** | GitHub Projects, Jira, Linear | Who's doing what, what's blocked |
| **Video updates** | Loom, Flip | Demo, status, complex explanations |
| **Sync meetings** | Zoom, Google Meet | Ceremonies, brainstorming, 1:1s |

> **Rule:** Use the **least synchronous tool** that works. Prefer doc over meeting. Prefer Loom over live demo.

## Ceremonies for Remote Teams

### Daily Standup (Async or Sync)

| Approach | How |
|----------|-----|
| **Async** | Written update in Slack/Teams channel by 10am. Read reviews for blockers. |
| **Sync (recommended)** | 15-min video call. Keep cameras on. Stick to the script. |

### Sprint Planning (Sync)

**Must be synchronous.** But share the prerequisite docs (backlog, priorities) 24 hours before:

- Record the meeting for absent team members
- Share the output in a written document
- Use a shared board (Miro, Linear, GitHub Projects)

### Sprint Review (Sync)

**Should be synchronous** for the demo. But:

- Pre-record demos for stakeholders who can't attend
- Share a written summary with links to what was shipped
- Collect async feedback with a deadline

### Retrospectives (Sync or Async)

| Remote Format | How |
|--------------|-----|
| **Async** (minimal) | Google Doc → everyone fills in Glad/Sad/Mad in 48 hours → facilitator synthesizes → team votes on actions |
| **Sync** (recommended) | Video call with shared Miro board. Use timer for each phase. Keep camera on. |

> **Tip:** For retros, sync is better. The conversation quality is higher. Async retros lose the emotional depth.

## Async Decision-Making

| Step | How Long | Action |
|------|----------|--------|
| 1. Propose | — | Write RFC or decision doc with clear options |
| 2. Feedback window | 24-48 hours | Tag relevant people. Write comments in the doc. |
| 3. Decision | After window | Author decides based on feedback. Writes conclusion. |
| 4. Announce | — | Post conclusion in public channel. Archive doc. |

### RFC (Request for Comments) Template

```markdown
## Title
What are we deciding?

## Context
Why does this decision need to be made?

## Options
### Option A
- Pros: ...
- Cons: ...

### Option B
- Pros: ...
- Cons: ...

## Recommendation
Which option and why?

## Timeline
Feedback by: [date]
Decision by: [date]
```

> **Tip:** Basecamp popularized async decision-making through their "Hill Charts" and writing culture. Every discussion starts with a written doc, not a meeting.

## Tools for Remote Teams

| Tool | What It's Good For |
|------|-------------------|
| **GitHub Projects / Linear** | Sprint tracking, roadmaps |
| **Notion / GitHub Wiki** | Documentation, RFCs, onboarding |
| **Slack / Teams** | Async chat, daily updates, channels |
| **Loom** | Async video updates, demo recordings |
| **Miro / Mural** | Remote retros, brainstorming, diagrams |
| **Donut (Slack app)** | Random 1:1 pairings, social connection |
| **Geekbot / Standuply** | Async standup bots (use with caution) |

## Time Zone Overlap

| Overlap | Strategy |
|---------|----------|
| 4+ hours | Shared standup, planning, retro. Rest is async. |
| 2-4 hours | Core hours for sync work. Everything else async. |
| 0-2 hours | Fully async. Record everything. Decisions are written. |
| No overlap | Async-first. One weekly sync meeting rotates time. |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Async by default but still expect replies in 5 minutes | Worst of both worlds | Set clear async norms and response time expectations |
| Too many meetings | No deep work time | Meeting-free days, async-first mindset |
| DMs for project decisions | Context lost | Public channels for everything project-related |
| No documentation culture | Tribal knowledge, onboarding pain | Write decisions down. Loom for complex topics. |
| Ignoring social connection | Isolation, low morale | Virtual coffee chats, team games, in-person retreats |
| Camera-off culture | Disconnect, low engagement | Cameras on for ceremonies. Be okay with off otherwise. |

## Related Topics

- [Sprint Execution](sprint-execution.md) — Adapting ceremonies for remote
- [Retrospectives](retrospectives.md) — Remote retro formats
- [Scrum](scrum.md) — The framework remains the same, the tools change

## Further Learning

- *Remote: Office Not Required* — Jason Fried & David Heinemeier Hansson
- *The Remote Book* — GitLab (free: about.gitlab.com/resources/ebook-remote/)
- [Basecamp's Guide to Remote Work](https://basecamp.com/books/remote)

---

> **Next:** [Troubleshooting](troubleshooting.md) | **Previous:** [Release Planning](release-planning.md)
