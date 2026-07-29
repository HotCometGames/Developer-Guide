# Docker Deployment

> Building production-grade Docker images and running them in deployment environments.

> **Related:** [Docker for Development](../08-virtual-environments/docker-for-development.md) | [Railway](railway.md) | [CI/CD Pipelines](ci-cd-pipelines.md)

---

## What Is It?

Docker packages your application and its runtime into a portable image. For deployment, the focus shifts from local development convenience to security, minimal image size, and production reliability.

## Multi-Stage Builds

Separate build dependencies from runtime dependencies:

```dockerfile
# Stage 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Production
FROM node:20-alpine AS runner
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm ci --only=production
EXPOSE 3000
CMD ["node", "dist/server.js"]
```

The final image contains only the compiled output and production dependencies — no TypeScript compiler, no dev dependencies, no source files.

## .dockerignore

```
node_modules
.git
.env
*.md
tests/
.dockerignore
Dockerfile
```

## Image Tagging Strategy

| Tag | When | Example |
|-----|------|---------|
| `latest` | Every deploy | `myapp:latest` |
| Git SHA | Every commit | `myapp:a1b2c3d` |
| Semver | Every release | `myapp:1.2.3` |
| Branch | Per-branch preview | `myapp:feature-login` |

```bash
docker build -t myapp:latest .
docker tag myapp:latest myapp:a1b2c3d
```

## Container Registry

```bash
# Push to Docker Hub
docker push myusername/myapp:latest

# Push to GitHub Container Registry
docker tag myapp:latest ghcr.io/myorg/myapp:latest
docker push ghcr.io/myorg/myapp:latest

# Push to AWS ECR
aws ecr get-login-password | docker login --password-stdin
docker push 123456.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
```

## Production Docker Compose

```yaml
# docker-compose.yml (production)
version: "3.9"
services:
  app:
    image: myapp:latest
    restart: always
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=${DATABASE_URL}
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
```

## Best Practices

| Practice | Why |
|----------|-----|
| Use Alpine-based images | Smaller attack surface, faster pulls |
| Multi-stage builds | Final image has only what's needed |
| Pin base image versions | `node:20-alpine` not `node:latest` |
| Run as non-root user | Security |
| Set `HEALTHCHECK` | Orchestrator knows if the app is alive |
| Use `.dockerignore` | Faster builds, fewer cache invalidations |
| Don't store secrets in images | Use runtime env vars or mounted secrets |

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Huge images | Slow deploys, expensive storage | Multi-stage builds, Alpine base |
| Running as root | Security vulnerability | Add `USER appuser` in Dockerfile |
| No health check | Orchestrator can't detect failures | Add `HEALTHCHECK` instruction |
| Building images in production | Inconsistent artifacts | Build once, promote same image |
| Hardcoded config | Can't run in multiple environments | Environment variables everywhere |

## What's Next?

Learn how to integrate Docker builds into [CI/CD Pipelines](ci-cd-pipelines.md), or use a platform like [Railway](railway.md) that handles container orchestration for you.
