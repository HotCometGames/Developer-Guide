# What Is Deployment?

> Making your software available to users — environments, strategies, and rollbacks.

> **Related:** [CI/CD Pipelines](ci-cd-pipelines.md) | [Environment Management](environment-management.md) | [GitHub Actions](../04-github/github-actions.md)

---

## What Is It?

Deployment is the process of delivering a software build to an environment where users can access it. A good deployment process is repeatable, auditable, and recoverable.

## Environments

| Environment | Purpose | Who Sees It |
|-------------|---------|-------------|
| Development | Local coding and debugging | You |
| Staging | Pre-production validation | Team, QA |
| Production | Live user traffic | Users |

Each environment should mirror production as closely as possible — same OS, same database version, same configuration approach.

## Deployment Strategies

```
Blue-Green:
   Users ──→ Blue (live)
             Green (idle)
             └── Deploy new version here → switch traffic

Canary:
   Users ──→ 90% Old
             10% New (monitor, then ramp up)

Rolling:
   Users ──→ [A] → [B] → [C]  (replace one instance at a time)
```

| Strategy | Downtime | Risk | Complexity |
|----------|----------|------|------------|
| Blue-green | None | Instant switch — bad version hits all | Medium |
| Canary | None | Gradual rollout — easy to abort | High |
| Rolling | None | One instance at a time | Medium |
| Recreate | Full downtime | Simple but users see downtime | Low |

## Rollback Plan

Every deploy should answer: "How do we undo this?"

| Approach | Speed | Requirements |
|----------|-------|-------------|
| Git revert + redeploy | Minutes | CI/CD pipeline |
| Platform rollback | Seconds | Vercel/Railway/Fly dashboard |
| Database rollback | Minutes | Reversible migrations |
| Feature flag toggle | Instant | Feature flag system |

## The Deployment Pipeline

```
Code push → Build → Test → Package → Stage → Deploy → Smoke test
    │         │       │        │       │        │         │
    └── commit   npm     pytest   docker   deploy   health
                  run              build    to       check
                  build             image   staging
```

## Best Practices

- **Deploy often, deploy small** — small changes are easier to roll back
- **Immutable artifacts** — build once, deploy the same artifact everywhere
- **Health checks** — the pipeline should verify the deploy succeeded
- **No manual steps** — everything in the pipeline is automated
- **Audit trail** — every deploy is logged with who, what, when, and the diff
- **Feature flags** — decouple deploy from release

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Deploying on Friday | Weekend firefighting | Deploy early in the week |
| Manual deployment steps | Human error | Automate everything |
| No staging environment | Production surprises | Match staging to production |
| Rebuilding in production | Different artifact than tested | Build once, promote across environments |
| Ignoring rollback | Can't recover from bad deploy | Test rollback regularly |

## What's Next?

Choose a platform: [GitHub Pages](github-pages.md) for static sites, [Vercel](vercel.md) for frontends, or [Railway](railway.md) for full-stack apps.
