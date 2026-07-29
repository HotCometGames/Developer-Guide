# Railway

> Full-stack deployment platform with databases, Dockerfile support, and zero-config workflows.

> **Related:** [Vercel](vercel.md) | [Docker Deployment](docker-deployment.md) | [Environment Management](environment-management.md)

---

## What Is It?

Railway is a deployment platform that supports full-stack apps with attached databases, automatic HTTPS, GitHub integration, and Dockerfile-based builds. It's well-suited for hobby projects, startups, and services that need more than just a static frontend.

## Getting Started

```bash
railway login           # authenticate with GitHub
railway init            # link project directory
railway up              # deploy
```

## Key Features

| Feature | Description |
|---------|-------------|
| **Automatic HTTPS** | Every service gets a `*.railway.app` URL |
| **Dockerfile support** | Deploy any language/runtime |
| **Built-in databases** | Postgres, MySQL, Redis, MongoDB |
| **Environment variables** | Dashboard or CLI |
| **Preview deploys** | Per-branch environments |
| **Automatic deploys** | Connected to GitHub repo |

## Databases

```bash
railway add postgres       # create Postgres database
railway add redis          # create Redis instance

# Get connection string as env variable
# Railway automatically injects DATABASE_URL, REDIS_URL, etc.
```

## Environment Variables

```bash
railway variables          # list all variables
railway variables set KEY=value   # set a variable

# Variables are automatically available at runtime
# Use environment-specific values with Railway environments
```

## Dockerfile Example

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

Railway detects the Dockerfile and builds the image automatically. No configuration needed.

## Custom Domains

```bash
railway domain            # list domains
railway domain add example.com   # add custom domain
```

## CI Integration

When connected to GitHub, Railway auto-deploys on push to the connected branch. No separate CI configuration is needed for basic workflows.

## Best Practices

- **Use Dockerfile for production** — more control than buildpacks
- **Attach databases via Railway** — don't run DB in the app container
- **Use environment variables for config** — never hardcode connection strings
- **Health checks** — Railway monitors your service; configure them for reliable restarts
- **Preview branches** — use separate environments for staging

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| No health check endpoint | Railway can't detect if the app is running | Add `/health` endpoint returning 200 |
| Large build context | Slow deploys | Use `.dockerignore` |
| Binding to wrong port | Deployment fails health checks | Use `process.env.PORT || 3000` |
| Not setting environment variables | App crashes at startup | Set all required vars before first deploy |

## What's Next?

Learn [Docker Deployment](docker-deployment.md) for production-ready Docker patterns, or see [CI/CD Pipelines](ci-cd-pipelines.md) for automated deployment workflows.
