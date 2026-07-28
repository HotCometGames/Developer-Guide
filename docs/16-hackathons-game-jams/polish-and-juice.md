# Polish & Juice

> The final 20% of the event that makes the difference between "it works" and "it works and I'm proud of it."

> **Related:** [Building the MVP](building-the-mvp.md) | [Time Management](time-management.md)

---

## What Is Polish?

Polish is anything that makes your project **feel intentional** — not just functional, but designed. It's the difference between a prototype and a demo.

**Polish is not more features.** It's making existing features look, feel, and sound better.

## The Polish Hierarchy

Focus on polish in this order — each layer makes the project incrementally better.

```
1. Stability      → No crashes, no blank screens
2. Feedback       → Every action has a visible response
3. Clarity        → Users understand what to do
4. Consistency    → Visual and interaction patterns are uniform
5. Personality    → Character, charm, voice
6. Extras         → Animations, effects, Easter eggs
```

## For Hackathons: UI Polish

### The 80/20 of UI Polish

| Change | Impact | Effort |
|--------|--------|--------|
| Consistent spacing and alignment | High | Low |
| Proper loading/error/empty states | High | Medium |
| Remove placeholder text | Medium | Low |
| One accent color throughout | Medium | Low |
| Favicon and page title | Medium | Low |
| Responsive layout (doesn't break on mobile) | High | Medium |
| Smooth transitions between pages | Medium | Low |
| Custom error page (not a stack trace) | High | Low |

### The 10-Minute UI Audit

Before submission, do this:

1. Open your app on a fresh browser/device
2. Look for **alignment issues** — are things where they should be?
3. Look for **blank states** — what happens if there's no data?
4. Look for **error states** — what if the API fails?
5. Look for **missing feedback** — does clicking a button do nothing?
6. Fix the worst three things in 10 minutes each.

## For Game Jams: Game Feel (Juice)

"Juice" is the collection of small effects that make a game feel responsive and satisfying. A game with juice is **fun to control even if the gameplay is simple.**

### The Juice Checklist

| Effect | How | Impact |
|--------|-----|--------|
| **Screen shake** | Shake the camera on impact | High |
| **Particles** | Burst on collision, collection, death | High |
| **Squash and stretch** | Scale on landing/jumping | High |
| **Sound effects** | Every interaction has a sound | High |
| **Visual feedback** | Button press, hit flash, pick-up glow | Medium |
| **Smooth camera** | Lerp follow, dead zone | Medium |
| **Trails** | Motion trails on player/projectiles | Medium |
| **Timing stops** | Freeze frame on impact | Low |

### Before and After

```
Without juice:
  Player touches coin → coin disappears, score +1

With juice:
  Player touches coin →
    Coin plays a 0.2s scale-up + rotation animation
    Particles burst in the coin's color
    A "+1" text floats up and fades
    A short "ding" sound plays
    The score number animates (scales up briefly)
```

> **Rule:** Add juice in order of player attention. Screen shake and SFX are the highest impact per minute invested.

## Audio: The Most Overlooked Polish

Audio adds more perceived quality than almost any visual change.

### Hackathon Audio

- [ ] App sounds for key actions (notification, error)
- [ ] Background music optional — skip if you're not a musician
- [ ] Use free SFX packs (kenney.nl, freesound.org)

### Game Jam Audio

- [ ] SFX for: jump, collect, damage, death, menu click
- [ ] A single looping background track
- [ ] Sound for win/lose state
- [ ] UI sounds (hover, click, back)

> **Tip:** If you don't have a musician, use [sfxr](https://www.drpetter.se/project_sfxr.html) or [ChipTone](https://sfbgames.itch.io/chiptone) to generate sounds in minutes.

## The "Last Hour" Checklist

When one hour remains:

```
□ Build the final version (release mode)
□ Test on a clean browser/device
□ Write the description/readme
□ Screenshot or record a demo video
□ Check that all links work
□ Submit
```

> **Rule:** Stop coding 30 minutes before submission. Use those 30 minutes to prepare the submission itself.

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Polishing before the feature works | Beautiful but broken | MVP first, polish last |
| Over-polishing one thing | A stunning button and nothing else works | Spread polish evenly |
| No audio | Low perceived quality | Add at least essential SFX |
| Ignoring loading states | App looks broken while loading | Add spinner/skeleton immediately |
| Forgetting the description | Great project, no one understands it | Write the pitch first, revise at end |

## Related Topics

- [Building the MVP](building-the-mvp.md) — Make it work before making it pretty
- [The Pitch & Demo](the-pitch-and-demo.md) — You'll need to show all this polish off

## Further Learning

- [Juice It or Lose It](https://www.youtube.com/watch?v=Fy0aCDmgnxg) — The original GDC talk on game feel
- [Game Feel: The Secret Sauce](https://www.youtube.com/watch?v=216_5nuEesQ) — GMTK

---

> **Next:** [The Pitch & Demo](the-pitch-and-demo.md) | **Previous:** [Building the MVP](building-the-mvp.md)
