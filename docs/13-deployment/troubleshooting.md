# Deployment Troubleshooting

> Common deployment failures and how to fix them.

---

## Build Failures

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Build succeeds locally, fails in CI | Environment differences | Match CI OS/node/Python versions to local |
| Out of memory in CI | Too many parallel builds | Reduce matrix parallelism, increase runner size |
| Cache miss every time | Cache key mismatch | Check cache key includes lockfile hash |
| Dependency install fails | Network issues or broken package | Retry, check package registry status |
| TypeScript build fails | Type errors not caught locally | Run `tsc --noEmit` locally first |

## Deployment Timeouts

| Problem | Fix |
|---------|-----|
| Build takes too long | Optimize Dockerfile (multi-stage, layer caching) |
| Upload times out | Compress artifact, reduce image size |
| Health check fails during deploy | Increase grace period, verify port binding |
| Database migration times out | Run migrations before deploying new code |
| Cold start too slow | Warmth keep-alive or increase reserved concurrency |

## DNS & Domain Issues

| Symptom | Cause | Fix |
|---------|-------|-----|
| Domain not resolving | DNS hasn't propagated | Wait up to 48 hours, verify with `dig` |
| "ERR_SSL_VERSION_OR_CIPHER_MISMATCH" | TLS misconfiguration | Check SSL/TLS settings on platform |
| Redirect loop | Misconfigured www vs non-www | Set canonical domain, redirect the other |
| Custom domain shows platform default URL | CNAME not set | Add CNAME record at DNS provider |

## Platform-Specific Issues

### GitHub Pages

| Problem | Fix |
|---------|-----|
| Files starting with `_` missing | Add `.nojekyll` file to output |
| 404 after deploy | Wait a few minutes for propagation |
| Custom domain not working | Verify CNAME in DNS and repo settings |

### Vercel

| Problem | Fix |
|---------|-----|
| Serverless function timeout | Increase limit, or move to longer-running endpoint |
| "Function deleted" | Serverless function idle timeout — warm or redesign |
| Build failed: no lockfile | Commit `package-lock.json` or `yarn.lock` |

### Railway

| Problem | Fix |
|---------|-----|
| App crashes immediately | Check logs for port binding issue |
| Database connection refused | Railway injects env vars — verify exact variable name |
| Build loop | Check for infinite restart due to crash |

## Rollback

```bash
# GitHub Pages — revert commit and push
git revert HEAD && git push origin master

# Vercel — list and promote
vercel list
vercel promote <deployment-id>

# Railway — rollback via dashboard
Railway Dashboard → Deployment → Rollback

# Docker — deploy previous image tag
docker run myapp:previous-tag
```

## Debugging Deployments

| Tool | When |
|------|------|
| `docker logs container` | Containerized app issues |
| Platform logs dashboard | Build and runtime errors |
| Health check endpoint | Application alive? |
| Staging environment | Reproduce without affecting production |
| Feature flag toggle | Disable problematic feature without redeploy |

## Best Practices to Prevent Issues

- **Test deployments to staging first** — catch environment-specific issues before production
- **Monitor after deploy** — error rates, latency, and traffic for 15 minutes post-deploy
- **Deploy during low traffic** — reduces user impact if something goes wrong
- **Automate rollback** — one command to revert to the previous working version
- **Keep a runbook** — document recurring deployment issues and their resolutions

---

> **Related:** [What Is Deployment?](what-is-deployment.md) — deployment fundamentals | [CI/CD Pipelines](ci-cd-pipelines.md) — pipeline troubleshooting
