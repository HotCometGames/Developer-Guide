# Building the MVP

> How to go from idea to working prototype fast — and resist the urge to build more than you need.

> **Related:** [Time Management](time-management.md) | [Choosing an Idea](choosing-an-idea.md) | [Polish & Juice](polish-and-juice.md)

---

## The MVP Mindset

> **"If you're not embarrassed by your MVP, you shipped too late."** — Reid Hoffman

Your goal is not a production-ready application. Your goal is **something that demonstrates your idea works** and makes people want to see what's next.

## Build Order

Build in this order, never skipping ahead:

```
1. Core mechanic     → Does the thing do the thing?
2. Happy path flow   → Can a user complete the primary task?
3. Minimal UI        → Can they figure out what to do?
4. Content           → Is there enough to demo?
5. Polish            → Does it look and feel intentional?
6. Edge cases        → Only if there's time
```

### Hackathon Build Order

| Step | What | Timebox |
|------|------|---------|
| 1. Skeleton | Repo init, build system, hello world | 30 min |
| 2. Data model | Schema, types, core objects | 1 hour |
| 3. One API endpoint | Full round-trip: UI → API → DB → response | 2 hours |
| 4. One full feature | Login + create + display a thing | 3 hours |
| 5. Remaining features | One by one, highest value first | Remaining time |
| 6. Polish | UI, error states, loading states | Last 20% |

### Game Jam Build Order

| Step | What | Timebox |
|------|------|---------|
| 1. Player movement | Can the player move and jump? | 1-2 hours |
| 2. Core interaction | What does the player DO? (shoot, collect, avoid) | 2-3 hours |
| 3. One level/scene | A complete gameplay loop | 2-3 hours |
| 4. Lose/win condition | Game ends somehow | 1 hour |
| 5. Content | More levels, enemies, obstacles | Remaining time |
| 6. Juice | Particles, screen shake, sfx | Last 20% |

## The Vertical Slice

Instead of building all the backend, then all the UI, then connecting them — build **one feature all the way through**:

```
❌ Wrong: Build all APIs → Build all UI → Connect everything → Panic
✅ Right: Login works end-to-end → Then: Create item works end-to-end → etc.
```

Each vertical slice is a complete feature:

```
[Database] → [API] → [Frontend] → [User sees it]
```

When you have one working vertical slice, you have momentum. Everything after that is repeating a proven pattern.

## The "Don't Rewrite" Rule

> **Never rewrite code during a hackathon.**

Your first attempt is messy. That's fine. The temptation to "clean it up" or "do it right" is strong, but every minute spent rewriting is a minute not spent on something that matters.

| Urge | Instead |
|------|---------|
| "This code is ugly" | Leave it. It works. Move on. |
| "Let me refactor first" | Add the next feature instead. |
| "I should use a better pattern" | Patterns matter in production. Not here. |
| "Let me restart with a fresh project" | No. Ship what you have. |

> **Exception:** If the current approach is fundamentally blocking progress (e.g., chosen framework literally can't do what you need), pivot fast. Delete only what you must.

## When to Pivot

Sometimes your idea doesn't work. Knowing when to change course is a skill.

| Sign | Action |
|------|--------|
| Core mechanic is unfun after 2 hours | Change the mechanic, not the theme |
| API doesn't exist or is too slow | Mock the data, build the UI anyway |
| Team is stuck on the same problem for 2 hours | Drop that feature. Build something else. |
| No one is excited about the idea | It won't get better. Cut scope or change direction. |

> **Pivot rule:** If you pivot, you have to be willing to ship something 50% smaller than your current plan. Pivoting costs time — you lose features.

## What "Done" Looks Like

### Hackathon MVP

```
- [ ] A user can open the app and understand what it does
- [ ] The core action works (submit, create, search, etc.)
- [ ] There's a visible result (data displayed, something changed)
- [ ] It runs without crashing 80% of the time
- [ ] You can demo it without showing the terminal
```

### Game Jam MVP

```
- [ ] Player can move and interact
- [ ] There's a clear goal or challenge
- [ ] Game can be won or lost
- [ ] It feels responsive (no input lag)
- [ ] It runs on the target platform
- [ ] There's some connection to the theme
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Building backend first | Nothing to show for 8 hours | Vertical slice — frontend + backend together |
| Too much abstraction | Wasting time on "clean architecture" | Monolith. Shove it in one file if you have to. |
| Edge case paralysis | Handling errors before the happy path works | Happy path first, errors second |
| Over-polishing | A button with 5 animation states and the feature doesn't work | Functional first, beautiful later |
| Not shipping | "Just one more feature" | Ship at feature freeze. Fix bugs only. |

## Related Topics

- [Polish & Juice](polish-and-juice.md) — Making your MVP look intentional
- [Time Management](time-management.md) — Staying on schedule through the build
- [Choosing an Idea](choosing-an-idea.md) — Before you build, choose well

## Further Learning

- *The Lean Startup* — Eric Ries (MVP philosophy)
- [How to Prototype a Game in Under 7 Days](https://www.youtube.com/watch?v=4le5nlI1R3w) — Extra Credits

---

> **Next:** [Polish & Juice](polish-and-juice.md) | **Previous:** [Tech Stack & Setup](tech-stack-and-setup.md)
