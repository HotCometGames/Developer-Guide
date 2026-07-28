# Docker for Development

> Using Docker for environment isolation during development — not deployment.

> **Related:** [Dev Containers](dev-containers.md) | [What Is a Virtual Environment?](what-is-a-virtual-environment.md)

---

## What Is It?

Docker packages your entire development environment into a container — the OS, runtime, tools, and dependencies. Unlike venv or nvm (which isolate a single language), Docker isolates at the operating system level. This page covers Docker as a *development* tool, not a deployment tool.

## Development vs Production Docker

| Aspect | Development Docker | Production Docker |
|--------|-------------------|-------------------|
| Goal | Reproducible dev environment | Run the app in production |
| Code mounting | Bind mount source code | Copy code into image |
| Hot reload | Yes (file watchers) | No |
| Debugging | Exposed ports, debuggers | Minimized attack surface |
| Image size | Can include dev tools | Minimized (distroless) |

## Dockerfile for Development

```dockerfile
FROM python:3.12-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Install Python dependencies (cached unless requirements change)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Default command
CMD ["python", "app.py"]
```

### Docker Compose

`docker-compose.yml` sets up the full development environment with services:

```yaml
services:
  app:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/app          # mount source code for live editing
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/myapp
    depends_on:
      - db

  db:
    image: postgres:16
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

## Development Commands

```bash
docker compose up -d          # start all services in background
docker compose up --build     # rebuild and start
docker compose logs -f        # follow logs
docker compose exec app bash  # shell into the app container
docker compose down           # stop and remove containers
docker compose down -v        # also remove volumes (fresh start)
```

## Benefits for Development

| Benefit | What It Means |
|---------|---------------|
| **Reproducible** | Same environment on every machine — no "works on my machine" |
| **Isolated** | Each project has its own OS, tools, and network |
| **Service dependencies** | Databases, caches, message queues run alongside the app |
| **Team onboarding** | `docker compose up` is all you need to start |
| **Test environments** | Spin up a clean environment for every test run |
| **Cleanup** | `docker compose down -v` — no leftover installs on your host |

## Common Patterns

### Development with Hot Reload

```dockerfile
# Use a dev server with auto-reload
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```

### Multiple Docker Compose Files

```bash
# Base config (always applied)
docker compose -f docker-compose.yml

# Dev overrides (add dev-specific settings)
docker compose -f docker-compose.yml -f docker-compose.dev.yml

# Test overrides
docker compose -f docker-compose.yml -f docker-compose.test.yml
```

### Root vs Rootless

By default, Docker runs containers as root. Files created inside the container may be owned by root on the host. Fix it:

```dockerfile
# Create a non-root user
RUN useradd -m -u 1000 devuser
USER devuser
```

Or use `--user` flag:

```bash
docker compose run --user $(id -u):$(id -g) app bash
```

## Pitfalls

| Mistake | Why | Fix |
|---------|-----|-----|
| Rebuilding instead of mounting | Code changes require rebuild | Mount the source directory with `volumes:` |
| Permission issues in mounted volumes | Container user != host user | Match UIDs or use `--user` |
| .dockerignore missing | Sends entire project to Docker daemon | Add `.dockerignore` with `node_modules/`, `.venv/`, `.git/` |
| Too large images | Installing unnecessary packages | Use slim images (`python:3.12-slim`), multi-stage builds |
| Hot reload slow on Windows/macOS | File system performance | Use WSL2 (Windows) or VirtioFS (macOS). Move source into WSL2 file system |

## When to Use Docker vs venv/nvm

| Scenario | Use |
|----------|-----|
| Python-only project | venv (+ pyenv if needed) |
| Need databases, caches, queues | Docker Compose |
| Mixed-language project | asdf or Docker |
| Reproducible CI environment | Docker (same image in CI and dev) |
| Team of one, simple project | venv/nvm |
| Team of many, complex project | Docker Compose or Dev Containers |
