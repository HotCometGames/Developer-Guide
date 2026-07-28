# Tech Stack & Setup

> Choosing tools you already know, pre-configuring your environment, and avoiding the #1 time sink — fighting your setup.

> **Related:** [Building the MVP](building-the-mvp.md) | [Time Management](time-management.md)

---

## The First Rule of Tech Stack

> **Use what you know.** A hackathon is not the time to learn a new framework. The 6 hours you save by using familiar tools can be the difference between shipping and failing.

## Stack Selection Criteria

| Criterion | Why | Green Flag | Red Flag |
|-----------|-----|------------|----------|
| **Familiarity** | No learning curve | You've shipped a project with it | "I watched a tutorial once" |
| **Setup time** | Time to hello world | Under 10 minutes | Takes 2 hours to configure |
| **Demo-ability** | Easy to show results | Visual, interactive | Backend-only, no UI |
| **Free tier** | No payment surprises | Fully free for your scale | Needs credit card |
| **Time to MVP** | Fast iteration | Core feature in 4 hours | Core feature takes 12 hours |
| **Hosting** | Easy deployment | One-click deploy | Manual server config |

## Recommended Stacks

### Hackathons

| Type | Stack | Why |
|------|-------|-----|
| **Web app** | Next.js + Tailwind + Supabase | Full-stack in one repo, auth included, free tier |
| **API** | FastAPI + SQLite + Render | Simple, Python, quick deploy |
| **Mobile** | React Native + Expo | Cross-platform, fast iteration |
| **CLI tool** | Python + Click + Typer | Zero UI, just works |
| **AI/ML** | Python + HuggingFace + Gradio | Pre-built models, easy demo UI |
| **Browser game** | Phaser.js + p5.js | No install, shareable link |

### Game Jams

| Type | Stack | Why |
|------|-------|-----|
| **2D** | Godot | Free, lightweight, great 2D tools |
| **3D** | Unity | Largest ecosystem, asset store |
| **Browser** | Phaser.js / PixiJS | No build step, instant share |
| **Retro** | PICO-8 / TIC-80 | Built-in constraints, tiny scope |
| **Text** | Twine / Ink | Narrative games, no art needed |
| **Prototype** | GameMaker | Fastest path to playable |

## Pre-Event Setup Checklist

Do this **before** the event starts:

### 1 Week Before

- [ ] Register for the event
- [ ] Form team and share contact info
- [ ] **Install and test** all tools on your machine
- [ ] Run the starter template / boilerplate end-to-end
- [ ] Verify deployment pipeline works (one-click deploy)
- [ ] Test with teammates — can everyone build and run the project?
- [ ] Download any assets you might need (free asset packs, sound libraries)

### Day Before

- [ ] Update everything (OS updates take forever mid-event)
- [ ] Charge all devices
- [ ] Set up your workspace (dual monitors, good lighting)
- [ ] Prepare snacks and water
- [ ] Write down your key commands and shortcuts
- [ ] Test internet connectivity at the venue
- [ ] Get a good night's sleep

## Boilerplates Worth Having

Keep these ready in a GitHub repo so you can clone and go:

### Hackathon Boilerplates

```
hackathon-boilerplate/
├── next-app/           # Next.js + Tailwind starter
├── fastapi-api/        # FastAPI + SQLite
├── react-native-app/   # Expo starter
└── python-cli/         # Click app scaffold
```

### Game Jam Boilerplates

```
jam-boilerplate/
├── godot-2d/           # Basic scene, player controller
├── unity-2d/           # Player movement, camera follow
├── phaser-game/        # Game loop, sprite loading
└── pico8-cart/         # Empty PICO-8 cart
```

> **Tip:** Keep these in a private GitHub repo or a USB drive. You never know if the venue's internet will hold up.

## Version Control

```bash
git init
git add .
git commit -m "Initial commit"
# Do this in the first 15 minutes, not the last 15 minutes
```

| Rule | Why |
|------|-----|
| Commit every working feature | Rollback if something breaks |
| Push to remote after every commit | Laptop dies = no project lost |
| One branch (main) is fine | No time for code review |
| Write meaningful commit messages | Helps teammates understand changes |

## Deployment

| Strategy | When | Tool |
|----------|------|------|
| **Continuous** | Use it as you build | Vercel, Railway, Render |
| **End** | Deploy once before submission | `vercel --prod` |
| **Self-hosted** | Only if necessary | DigitalOcean, fly.io |

> **Tip:** Deploy early. Deploy often. A broken deployment discovered 30 minutes before submission is a nightmare. If possible, enable auto-deploy from your repo's main branch.

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Trying a new stack | Hours wasted on learning curve | Use what you know |
| No pre-setup | First 2 hours installing tools | Set up everything before the event |
| No boilerplate | Reimplementing auth/routing every time | Keep starter templates ready |
| No deployment testing | Deploy fails at submission time | Deploy first, ask questions later |
| Ignoring offline access | Venue wifi fails | Have offline-capable tools, hotspot plan |
| Over-engineering | Complex architecture for a 24h project | Monolith first, extract only if needed |

## Related Topics

- [Building the MVP](building-the-mvp.md) — What you'll build with your stack
- [Time Management](time-management.md) — Setup time is part of your budget

## Further Learning

- [Awesome Hackathon Tools](https://github.com/benawad/hackathon-starter) — Community-curated boilerplates
- [Free Game Assets](https://itch.io/game-assets/free) — Kenney, OpenGameArt, Freesound

---

> **Next:** [Building the MVP](building-the-mvp.md) | **Previous:** [Time Management](time-management.md)
