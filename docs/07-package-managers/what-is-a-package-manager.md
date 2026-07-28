# What Is a Package Manager?

> A tool that automates installing, updating, configuring, and removing software dependencies.

> **Related:** [Lockfiles & Supply Chain Security](lockfiles-and-security.md) | [Virtual Environments](../08-virtual-environments/README.md)

---

## What Is It?

A package manager handles the logistics of using third-party code. It downloads packages from a registry, resolves their dependencies, ensures compatible versions, and provides commands to install, update, and remove them.

## Core Concepts

### Registry

A registry is a server that hosts packages. When you install a package, the package manager downloads it from a registry.

| Ecosystem | Default Registry |
|-----------|-----------------|
| JavaScript | npmjs.com |
| Python | pypi.org |
| Rust | crates.io |
| Go | proxy.golang.org |
| .NET | nuget.org |

### Lockfile

A lockfile records the exact versions of every dependency (and their dependencies) that were installed. Committing the lockfile ensures everyone gets the same versions — "works on my machine" becomes "works on every machine."

### Semantic Versioning (SemVer)

Most ecosystems use semver: `MAJOR.MINOR.PATCH`.

| Change | Example | What It Means |
|--------|---------|---------------|
| Major | `2.0.0` | Breaking changes |
| Minor | `1.3.0` | New features, backward-compatible |
| Patch | `1.2.4` | Bug fixes, backward-compatible |

### Version Ranges

```json
// npm — flexible range
"react": "^18.2.0"    // >=18.2.0 and <19.0.0
"react": "~18.2.0"    // >=18.2.0 and <18.3.0
"react": "18.2.0"     // exact version only

// Rust — exact by default
[dependencies]
serde = "1.0"         // >=1.0.0 and <2.0.0

// Go — tagged versions
require github.com/pkg/errors v0.9.0
```

## How Dependency Resolution Works

1. Read the dependency manifest (`package.json`, `Cargo.toml`, `pyproject.toml`)
2. For each dependency, check what versions satisfy the range
3. Recursively resolve sub-dependencies
4. Check for version conflicts (two packages requiring different versions of the same dependency)
5. Generate a lockfile with exact version pins
6. Download and install packages to a local cache

## Package Manager vs Build System

Some ecosystems combine package management with building:

| Tool | Package Manager? | Build System? |
|------|----------------|---------------|
| npm | Yes | No (scripts only) |
| cargo | Yes | Yes |
| Go modules | Yes | Yes (via `go build`) |
| pip | Yes | No |
| poetry | Yes | Yes |

## Lockfile & Manifest

| File | What It Contains | Committed? |
|------|-----------------|------------|
| `package.json` | Direct dependencies + version ranges | Yes |
| `package-lock.json` | Exact resolved versions for all deps | Yes |
| `Cargo.toml` | Direct dependencies + version ranges | Yes |
| `Cargo.lock` | Exact resolved versions | Yes |
| `go.mod` | Module path + direct dependencies | Yes |
| `go.sum` | Cryptographic hashes of dependencies | Yes |
| `requirements.txt` | Pinned versions (pip convention) | Yes |

## What's Next?

Explore package managers by ecosystem: [JavaScript](javascript-package-managers.md), [Python](python-package-managers.md), [Cargo](cargo.md), or [Go Modules](go-modules.md).
