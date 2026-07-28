# Hackathons & Game Jams Troubleshooting

> Common problems during events — and how to handle them without losing your mind or the project.

> **Related:** [Time Management](time-management.md) | [Building the MVP](building-the-mvp.md) | [Team Formation & Roles](team-formation-and-roles.md)

---

## How to Diagnose in the Moment

When something goes wrong during an event, ask:

1. **Can I fix this in 30 minutes?** If yes, fix it. If no, cut it or find a workaround.
2. **Does this block the core feature?** If no, defer it. If yes, swarm on it.
3. **Will the judges notice?** If no, skip it. If yes, find a minimal fix.

---

## Problem: Over-Scoping

> You planned too much. The core feature isn't working. You're 60% through the event and have 40% of the planned features done.

**Symptoms:**

- Task board is full of half-done features
- Team is stressed and working on different things
- Nothing is demo-ready

**How to fix:**

1. **Call a 5-minute team huddle.** "We're over-scoped. What's the one thing we need to demo?"
2. **Cut everything except the core feature.** Anything not essential goes to "maybe if there's time."
3. **Swarm on one thing.** Everyone works on the same feature until it works.
4. **Accept the loss.** You won't build everything. Ship a smaller, working project.

> **Prevention:** Use the scope cutting guide in [Time Management](time-management.md) from the start.

## Problem: Tech Stack Failure

> A tool, library, or API isn't working as expected. You've wasted hours on it.

**Symptoms:**

- Same Stack Overflow tab open for 2 hours
- "It should be simple but it's not working"
- Team morale is dropping

**How to fix:**

1. **30-minute rule.** If stuck for 30 minutes, switch approaches.
2. **Find a simpler alternative.** Can you mock the data? Use a different library? Skip the feature?
3. **Ask for help.** Event Discord, Stack Overflow, teammate who knows the stack.
4. **Pivot.** If the stack fundamentally can't do what you need, change stacks NOW. The earlier you accept this, the better.

### Common Tech Failures

| Failure | Quick Fix |
|---------|-----------|
| API rate limit | Add a cache or mock |
| Deployment failing | Use a different platform (Vercel → Railway) |
| Library doesn't work | Drop it and write a simpler version |
| Auth is too complex | Use a one-click auth provider (Auth0, Supabase) |
| Database schema wrong | SQLite — just delete and recreate. No migrations. |
| Git merge conflict | `git checkout --ours` and move on |

## Problem: Team Conflict

> Disagreements, unequal contribution, or communication breakdown.

**Symptoms:**

- People stop talking
- Someone is working on something nobody agreed on
- "I'm doing everything" sentiment

**How to fix:**

1. **Take 5 minutes to realign.** "Let's quickly agree on what we're building and who's doing what."
2. **Reassign roles.** If someone is stuck or unhappy, swap tasks.
3. **Compromise.** "We'll do it your way for now. We can change it if there's time."
4. **Don't escalate.** It's 48 hours. You don't need to resolve deep issues — you need to ship.

> **Prevention:** Clear role assignment from the start (see [Team Formation & Roles](team-formation-and-roles.md)).

## Problem: Burnout / Energy Crash

> You hit a wall. Can't think clearly. Everything feels hopeless.

**Symptoms:**

- Staring at the screen, not coding
- Irritability with teammates
- Making silly mistakes
- "I don't care anymore"

**How to fix:**

1. **Step away.** 20-minute walk. No phone. No code.
2. **Eat something real.** Not just energy drinks and candy.
3. **Sleep.** Even 45 minutes resets your brain.
4. **Talk to someone.** Vent to a teammate. The emotional release helps.
5. **Do an easy task.** Fix a typo, add a comment, make a simple CSS change. Get a small win.

> **Prevention:** Plan breaks into your schedule. Sleep is part of the strategy, not a failure.

## Problem: Demo Disaster

> The app crashes, won't load, or the feature doesn't work during the pitch.

**Symptoms:**

- Blank screen on stage
- "It worked 5 minutes ago"
- Sweating

**How to fix:**

1. **Play the backup video.** (You recorded one, right?)
2. **Describe it confidently.** "What you'd see here is..." — walk through what it does.
3. **Own it.** "We hit a last-minute bug during submission. Here's what we built and why we're excited about it."
4. **Show screenshots.** If you have any, throw one on screen.

> **Prevention:** See [The Pitch & Demo](the-pitch-and-demo.md) — always have a backup recording.

## Problem: Theme Doesn't Fit

> You realized your game doesn't actually connect to the jam theme.

**Symptoms:**

- Judges say "I don't see how this relates to the theme"
- You're scrambling to add theme elements in the last hour

**How to fix:**

1. **Add a thematic element in the UI.** A title screen, a line of dialogue, a visual motif.
2. **Change the narrative.** Reframe what the game is about in your description.
3. **Don't overhaul mechanics.** Changing mechanics at hour 40 is suicide. Change the presentation instead.

> **Prevention:** Before committing to an idea, ask: "Can I explain how this connects to the theme in one sentence?"

## Problem: Version Control Disaster

> Lost work, merge conflicts, corrupted repo.

**Symptoms:**

- `git push --force` was involved
- "Wait, where did my code go?"
- Team members have different versions

**How to fix:**

1. `git reflog` — find the commit you need
2. `git reset --hard <hash>` — go back to a known good state
3. If that fails, use a file recovery tool or re-create from memory
4. **From now on:** commit every 30 minutes

> **Prevention:** First 10 minutes of the event: `git init`, `git add .`, `git commit -m "init"`, push to remote.

---

## Quick Reference

| Problem | Emergency Fix | Long-Term Fix |
|---------|---------------|---------------|
| Over-scoped | Cut all but the core feature | Plan with the "half it twice" rule |
| Tech failure | Switch to simpler alternative | Pre-test your stack before the event |
| Team conflict | Realign roles, compromise | Clear role assignment from start |
| Burnout | Walk, eat, sleep | Schedule breaks, sleep plan |
| Demo fails | Play backup video | Record a backup before the pitch |
| Theme mismatch | Add UI/narrative connection | Check theme fit before building |
| Git disaster | `git reflog`, find good commit | Commit every 30 minutes |

## Related Topics

- [Time Management](time-management.md) — Avoiding the time crunches that cause these problems
- [Team Formation & Roles](team-formation-and-roles.md) — Setting up for success before the event

## Further Learning

- [Post-Mortem Collection](https://gamejams.nicollazz.dev/) — Real game jam post-mortems

---

> **Previous:** [Post-Hackathon](post-hackathon.md) | **Next:** [Developer Wisdom](../17-developer-wisdom/README.md)
