# Deployment Quick Reference

> One-page reference for Docker, CI/CD, GitHub Actions, and deployment platforms. Print this or bookmark it.

---

## Docker

### Images

| Task | Command |
|------|---------|
| Build | `docker build -t name:tag .` |
| Build (no cache) | `docker build --no-cache -t name:tag .` |
| List images | `docker images` |
| Remove image | `docker rmi name` |
| Pull image | `docker pull name:tag` |
| Push image | `docker push name:tag` |
| Inspect | `docker inspect name` |
| Logs | `docker logs container` |
| Follow logs | `docker logs -f container` |

### Containers

| Task | Command |
|------|---------|
| Run | `docker run name:tag` |
| Run (detached) | `docker run -d name:tag` |
| Run (interactive) | `docker run -it name:tag sh` |
| Run (port) | `docker run -p 8080:80 name:tag` |
| Run (env) | `docker run -e KEY=val name:tag` |
| Run (volume) | `docker run -v host:container name:tag` |
| List running | `docker ps` |
| List all | `docker ps -a` |
| Stop | `docker stop container` |
| Start | `docker start container` |
| Restart | `docker restart container` |
| Remove | `docker rm container` |
| Exec | `docker exec -it container sh` |
| Copy | `docker cp container:path local` |

### Docker Compose

| Task | Command |
|------|---------|
| Up (detached) | `docker compose up -d` |
| Down | `docker compose down` |
| Build | `docker compose build` |
| Rebuild | `docker compose up -d --build` |
| Logs | `docker compose logs` |
| Follow logs | `docker compose logs -f` |
| Ps | `docker compose ps` |
| Exec | `docker compose exec service sh` |
| Restart | `docker compose restart` |
| Stop | `docker compose stop` |
| Pull | `docker compose pull` |

### Dockerfile Template

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

## GitHub Actions

### Workflow Template

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
      - run: npm ci
      - run: npm test

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run build
      # deploy step here
```

### Common Actions

| Action | Purpose |
|--------|---------|
| `actions/checkout@v4` | Clone repo |
| `actions/setup-node@v4` | Install Node |
| `actions/setup-python@v5` | Install Python |
| `actions/upload-artifact@v4` | Upload files |
| `actions/download-artifact@v4` | Download files |
| `actions/cache@v4` | Cache dependencies |
| `docker/build-push-action@v5` | Build & push Docker |
| `peaceiris/actions-gh-pages@v4` | Deploy to GitHub Pages |

### Useful Triggers

```yaml
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * 1'  # Weekly Monday 2am
  workflow_dispatch:       # Manual trigger
```

## Deployment Platforms

### Vercel

| Task | Command |
|------|---------|
| Install | `npm i -g vercel` |
| Deploy | `vercel` |
| Deploy prod | `vercel --prod` |
| Env set | `vercel env add KEY value` |
| Env pull | `vercel env pull .env.local` |
| Domains | `vercel domains add domain.com` |
| Logs | `vercel logs url` |

### Railway

| Task | Command |
|------|---------|
| Login | `railway login` |
| Init | `railway init` |
| Deploy | `railway up` |
| Logs | `railway logs` |
| Shell | `railway shell` |
| Variables | `railway variables` |
| Domain | `railway domain` |

### Fly.io

| Task | Command |
|------|---------|
| Login | `fly auth login` |
| Launch | `fly launch` |
| Deploy | `fly deploy` |
| Status | `fly status` |
| Logs | `fly logs` |
| Scale | `fly scale count 2` |
| SSH | `fly ssh console` |

## Environment Variables

### Management

| Platform | Set | Pull |
|----------|-----|------|
| Docker | `-e KEY=val` or `.env` | — |
| GitHub Actions | Repository Settings | — |
| Vercel | Dashboard or CLI | `vercel env pull` |
| Railway | Dashboard or CLI | `railway variables` |
| .env file | `KEY=val` | `.env.example` (committed) |

### .env File Rules

```gitignore
# .gitignore
.env
.env.local
.env.*.local

# .env.example (COMMITTED - shows required vars)
DATABASE_URL=
API_KEY=
SECRET_KEY=
```

## Rollback Strategies

| Strategy | How | When |
|----------|-----|------|
| Git revert | `git revert HEAD && git push` | Bad commit deployed |
| Platform rollback | Rollback button in dashboard | Immediate need |
| Blue-green | Switch traffic to old version | Zero-downtime rollback |
| Canary | Shift % to old version | Gradual rollback |
| Database rollback | Reverse migration | Schema changes |

## Common Workflows

### Deploy to Vercel from GitHub

```bash
# One-time setup
vercel link
vercel env add DATABASE_URL

# Automatic: Push to main triggers deploy
git push origin main

# Manual
vercel --prod
```

### Deploy Docker to Railway

```bash
railway login
railway init
railway up
railway domain
```

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm test
      - run: npm run build
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-args: '--prod'
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Hardcoded secrets in code | Leaks credentials | Use env vars + .gitignore |
| Large Docker images | Slow deploys | Use multi-stage builds, alpine |
| No health checks | Silent failures | Add `HEALTHCHECK` in Dockerfile |
| No rollback plan | Can't recover from bad deploy | Test rollback strategy |
| Deploying on push to main | Broken prod | Require PR reviews + passing CI |
| No .env.example | Team doesn't know config | Commit `.env.example` with dummy values |

---

> **Full section:** [Deployment](../13-deployment/README.md) | **Next:** [Game Development](gamedev-quick-reference.md)
