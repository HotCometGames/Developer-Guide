# Environment Management

> Configuring applications for development, staging, and production without changing code.

> **Related:** [What Is Deployment?](what-is-deployment.md) | [CI/CD Pipelines](ci-cd-pipelines.md) | [Docker Deployment](docker-deployment.md)

---

## What Is It?

Environment management is the practice of making an application behave differently in different environments (dev, staging, production) using external configuration — never code changes.

## The Twelve-Factor App — Config

From [12factor.net/config](https://12factor.net/config):

> Store config in the environment — strict separation of config from code.

## Environment Variables

The standard mechanism for passing configuration to applications:

```bash
# Development (.env)
DATABASE_URL=sqlite:///dev.db
API_KEY=dev-key-123
LOG_LEVEL=debug

# Production (set by platform)
DATABASE_URL=postgres://user:pass@host:5432/db
API_KEY=prod-key-456
LOG_LEVEL=info
```

## .env Conventions

| File | Purpose | Committed |
|------|---------|-----------|
| `.env.example` | Documents required variables | Yes |
| `.env` | Personal development config | No |
| `.env.local` | Local overrides | No |
| `.env.production` | Production values | No |

```gitignore
# .gitignore
.env
.env.*.local
```

## Secrets Management

| Approach | Best For | Example |
|----------|----------|---------|
| Platform dashboard | Simple projects | Vercel, Railway UI |
| CI secrets | Pipeline secrets | GitHub Actions secrets |
| Vault | Team/compliance | HashiCorp Vault |
| Encrypted files | Offline/air-gapped | `sops`, `git-crypt` |

```yaml
# GitHub Actions secrets
- name: Deploy
  env:
    DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
  run: docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
```

## Environment-Specific Config

```python
# settings.py
import os

ENV = os.getenv("APP_ENV", "development")

DATABASE_URL = os.getenv("DATABASE_URL")
DEBUG = ENV == "development"
LOG_LEVEL = os.getenv("LOG_LEVEL", "INFO" if ENV == "production" else "DEBUG")
```

```javascript
// config.js
export const config = {
  env: process.env.NODE_ENV || 'development',
  database: {
    url: process.env.DATABASE_URL,
  },
  api: {
    key: process.env.API_KEY,
  },
};
```

## Platform-Specific Config

| Platform | How to Set Variables |
|----------|---------------------|
| Vercel | Dashboard or `vercel env add` |
| Railway | Dashboard or `railway variables set` |
| GitHub Actions | Repository > Settings > Secrets and variables |
| Docker | `-e KEY=val` or `--env-file` |
| Docker Compose | `environment:` or `env_file:` in YAML |

## Best Practices

- **Fail fast on missing variables** — validate at startup, crash with a clear message
- **Never hardcode secrets** — not even in `.env.example`
- **Use sensible defaults** — for development only, never for production
- **Document required variables** — `.env.example` with placeholder values
- **Keep config minimal** — too many env vars is as bad as too few

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Committing `.env` | Secret leaked to repository | Add to `.gitignore`, remove from history |
| No `.env.example` | New devs don't know what to set | Commit example with placeholder values |
| Defaults in production | Oops-I-used-dev-config | Fail on missing production vars |
| Too many env vars | Configuration is opaque | Group related config, use reasonable defaults |
| Typed config as strings | Parsing errors in production | Validate and cast at startup |

## What's Next?

Apply these patterns when deploying to [Vercel](vercel.md), [Railway](railway.md), or through [CI/CD Pipelines](ci-cd-pipelines.md).
