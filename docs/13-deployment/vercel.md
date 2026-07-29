# Vercel

> Frontend deployment platform with previews, serverless functions, and zero-config builds.

> **Related:** [Railway](railway.md) | [Environment Management](environment-management.md) | [CI/CD Pipelines](ci-cd-pipelines.md)

---

## What Is It?

Vercel is a platform optimized for frontend frameworks (Next.js, SvelteKit, Nuxt) with automatic HTTPS, preview deployments for every branch, and serverless edge functions.

## Getting Started

```bash
npm install -g vercel
vercel login
vercel            # deploy preview
vercel --prod     # deploy to production
```

## Key Concepts

| Feature | Description |
|---------|-------------|
| **Previews** | Every branch/push gets a unique URL |
| **Auto-detection** | Detects framework (Next.js, Vite, etc.) and configures build |
| **Serverless Functions** | `/api/*.ts` files become HTTP endpoints |
| **Edge Functions** | Run at CDN edge nodes (low latency globally) |
| **Analytics** | Speed insights and web vitals |

## Configuration

```json
// vercel.json
{
  "framework": "nextjs",
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "installCommand": "npm ci",
  "env": {
    "NEXT_PUBLIC_API_URL": "@api_url"
  }
}
```

## Environment Variables

```bash
vercel env add DATABASE_URL     # prompt for value
vercel env add API_KEY production   # scoped to production
vercel env pull .env.local      # download for local dev
```

| Scope | Available In |
|-------|-------------|
| Production | Production deploy only |
| Preview | Preview deploys |
| Development | Local `vercel dev` |

## Serverless Functions

```typescript
// api/hello.ts
export default function handler(req, res) {
  res.json({ message: "Hello from Vercel!" });
}
```

Functions scale to zero when not in use — no servers to manage.

## Custom Domains

```bash
vercel domains add yourdomain.com
```

## CI Integration

Vercel auto-deploys when connected to a Git repository. For manual CI:

```yaml
# .github/workflows/deploy.yml
- name: Deploy to Vercel
  uses: amondnet/vercel-action@v25
  with:
    vercel-token: ${{ secrets.VERCEL_TOKEN }}
    vercel-args: '--prod'
```

## Best Practices

- **Use automatic Git integration** — each PR gets a preview URL automatically
- **Preview environments for everything** — let stakeholders see changes before merge
- **Set environment variables via CLI or dashboard** — never commit secrets
- **Use `.vercelignore`** to exclude unnecessary files from deployments
- **Configure a production domain** — preview URLs are long and random

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Committing `.env` files | Secret leakage | Use `vercel env` or dashboard |
| Not setting `NODE_VERSION` | Build failures from unexpected Node version | Set `engines` in `package.json` |
| Ignoring preview deploys | Merge breaks production | Check preview before merging |
| Overusing serverless functions | Cold starts impact UX | Use edge functions for latency-sensitive paths |

## What's Next?

For full-stack apps that need a database, see [Railway](railway.md). For CI/CD patterns, see [CI/CD Pipelines](ci-cd-pipelines.md).
