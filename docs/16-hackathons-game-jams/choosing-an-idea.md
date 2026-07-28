# Choosing an Idea

> The most important decision you'll make in the first hour — pick the right idea and everything else gets easier.

> **Related:** [Team Formation & Roles](team-formation-and-roles.md) | [Building the MVP](building-the-mvp.md)

---

## The Golden Rule

> **Your first idea is too big. Your second idea is probably too big too. Your third idea, after cutting scope twice, might be right.**

Scope is the #1 killer of hackathon projects. A small, polished project beats a grand, broken one every time.

## For Hackathons: Brainstorming

### Technique 1: Problem-First

Think of a specific problem you or someone you know has. Build the simplest possible solution.

| Good | Too Big |
|------|---------|
| "I forget to water my plants — build a moisture sensor + alert" | "Build a smart home automation platform" |
| "Finding cheap flights takes too long — build a price tracker" | "Build a travel booking marketplace" |

### Technique 2: Dogfooding

Build something you'd actually use. You'll stay motivated because you want the result.

```
Ask: "What's a task I do manually that I could automate in 12 hours?"
```

### Technique 3: API Remix

Pick an interesting API and build something on top of it. The API does the heavy lifting; you just wire up the UI.

| API | Idea |
|-----|------|
| GitHub API | "Show me which PRs are blocking my team" |
| Spotify API | "Generate a playlist from the BPM of my running pace" |
| OpenAI API | "Summarize my Slack messages into a daily digest" |

## For Game Jams: Theme Analysis

When the theme is announced, resist the urge to take the first idea. Spend 30 minutes exploring:

### Step 1: Interpret the Theme

Write down different angles for the theme. Don't filter yet.

```
Theme: "Growth"

Angles:
  - A plant growing (literal)
  - A character growing up (coming of age)
  - Your resources grow over time (incremental game)
  - Everything grows except the player (shrinking mechanic)
  - Emotional growth — a story about change
  - Infestation — mold, infection, uncontrolled growth
```

### Step 2: Filter

| Criterion | Question |
|-----------|----------|
| **Executable** | Can I make this in 48 hours? |
| **Fun** | Would I want to play this? |
| **Theme fit** | Does it clearly connect to the theme? |
| **Unique** | Is it different from the obvious interpretation? |

> **Tip:** The best jam games often take a **twist** on the theme rather than the literal interpretation. "Growth" → a lantern that shrinks unless you feed it light.

### Step 3: Lock It

Commit to one idea. Don't second-guess. Ideas are cheap — execution is everything.

```mermaid
graph LR
    A[Theme announced] --> B[Brainstorm 10+ ideas]
    B --> C[Filter to 3]
    C --> D[Discuss with team]
    D --> E[Pick one and GO]
    E -.->|No switching| F[Ship it]
```

## Feasibility Check

Before committing, answer these:

| Question | Green Light | Red Flag |
|----------|-------------|----------|
| Core mechanic works in 4 hours? | Yes | No — rethink |
| You know the tech stack? | Used it before | Learning it first time |
| Can you demo a prototype? | Yes | It's a backend-only API |
| Scope fits in 40% of total time? | Yes | Cut features now |

> **Rule:** If the core mechanic takes longer than 4 hours to prototype, the idea is too ambitious. Pick something simpler.

## The "One Thing" Rule

Ask: **What is the ONE thing this project must do to be successful?**

- Focus 80% of your time on that one thing
- Cut everything that doesn't serve it
- If that one thing doesn't work, nothing else matters

```
Hackathon: "One thing = a logged-in user can create a workout plan"
  - Authentication? Use OAuth/Magic links — skip custom auth
  - Social sharing? Nice to have — cut it
  - Analytics dashboard? No — just a list view

Game Jam: "One thing = the player can jump between moving platforms"
  - Level select? Cut — just one endless level
  - Power-ups? Cut — add if there's time
  - Enemies? Cut — they'd distract from the platforming
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Building what exists | Wasting time reinventing wheels | Use existing APIs, boilerplates, assets |
| Too many features | Nothing ships | Cut to one core feature |
| No theme connection | Judges mark you down | Map every feature back to the theme |
| Copying the obvious idea | Hard to stand out | Add a twist or combine two ideas |
| Switching ideas mid-event | Lost time, nothing finished | Commit and execute |

## Related Topics

- [Building the MVP](building-the-mvp.md) — Turning the idea into working software
- [Time Management](time-management.md) — Pacing yourself through the build

## Further Learning

- *The Mom Test* — Rob Fitzpatrick (customer discovery, relevant for hackathon ideas)
- [Game Design: How to Brainstorm Ideas](https://www.youtube.com/watch?v=6gdN0tR6lPs) — GMTK video on game jam ideation

---

> **Next:** [Team Formation & Roles](team-formation-and-roles.md) | **Previous:** [What Are Hackathons & Game Jams?](what-are-hackathons-and-game-jams.md)
