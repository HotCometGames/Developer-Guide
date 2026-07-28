# JavaScript Package Managers

> npm, yarn, pnpm, and bun — the JavaScript ecosystem's dependency management tools.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [Lockfiles & Supply Chain Security](lockfiles-and-security.md)

---

## What Is It?

The JavaScript ecosystem has more package managers than any other language. Each tool takes a different approach to the same problem: installing, resolving, and caching dependencies from the npm registry.

## The Options

### npm

The default, bundled with Node.js.

| Feature | Details |
|---------|---------|
| Lockfile | `package-lock.json` |
| Install strategy | Flat `node_modules` (nesting as needed) |
| Workspaces | Yes — monorepo support |
| Audit | `npm audit` |
| Cache | `~/.npm` |
| CI install | `npm ci` (frozen lockfile, no resolution) |

```bash
npm init -y               # create package.json
npm install react          # install and save to dependencies
npm install -D jest        # install as dev dependency
npm ci                     # clean install from lockfile (CI)
npm audit                  # check for vulnerabilities
```

### yarn

Meta's alternative, focused on speed and reliability.

| Feature | Details |
|---------|---------|
| Lockfile | `yarn.lock` |
| Install strategy | Flat with deterministic algorithm |
| Workspaces | Yes |
| Plug'n'Play | Optional — skip `node_modules` entirely |
| CI install | `yarn install --frozen-lockfile` |

```bash
yarn init -y
yarn add react
yarn add -D jest
yarn install --frozen-lockfile   # CI
yarn dlx create-react-app        # run binary without installing
```

### pnpm

Fast, disk-efficient — uses hard links and symlinks to avoid duplicating packages.

| Feature | Details |
|---------|---------|
| Lockfile | `pnpm-lock.yaml` |
| Install strategy | Content-addressable store, symlinked `node_modules` |
| Disk usage | Single copy of each package version (hard links) |
| Strict | `node_modules` only has direct dependencies |
| Workspaces | Yes (excellent monorepo support) |
| CI install | `pnpm install --frozen-lockfile` |

```bash
pnpm init
pnpm add react
pnpm add -D jest
pnpm install --frozen-lockfile
pnpm dlx create-react-app
```

### bun

A JavaScript runtime that bundles its own package manager, built in Zig for speed.

| Feature | Details |
|---------|---------|
| Lockfile | `bun.lockb` (binary) |
| Speed | Fastest install times |
| Compatibility | Reads `package.json`, can use `node_modules` |
| Native | Built into the bun runtime |

```bash
bun init
bun add react
bun add -D jest
bun install
```

## Comparison

| Feature | npm | yarn | pnpm | bun |
|---------|-----|------|------|-----|
| Install speed | OK | Good | Good | Fastest |
| Disk efficiency | Low | Low | High | Medium |
| Strictness | Low | Medium | High | Medium |
| Monorepo support | Workspaces | Workspaces | Excellent | Workspaces |
| Maturity | Highest | High | Medium | New |
| Runtime included | No | No | No | Yes |

## Choosing the Right One

| Use Case | Recommendation |
|----------|---------------|
| Standard project | npm (zero setup) |
| Monorepo | pnpm or yarn |
| Disk-space constrained | pnpm |
| Need maximum speed | bun |
| Team standardization | Any — use `packageManager` field in `package.json` |

Pin the package manager in `package.json`:

```json
{
  "packageManager": "pnpm@9.0.0"
}
```

## Lockfile Strategies

```bash
# npm
npm ci                    # respect lockfile exactly
npm install               # may update lockfile

# yarn
yarn install --frozen-lockfile  # fail if lockfile changes

# pnpm
pnpm install --frozen-lockfile  # fail if lockfile changes
```

- **Commit all lockfiles** — this is not optional
- **Use frozen-lockfile in CI** — prevents surprises
- **Review lockfile diffs in PRs** — unexpected changes may indicate a malicious package
