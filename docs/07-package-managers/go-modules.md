# Go Modules

> Go's built-in dependency management system — modules, versioning, and the proxy protocol.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [Lockfiles & Supply Chain Security](lockfiles-and-security.md)

---

## What Is It?

Go modules are Go's native dependency management system. Introduced in Go 1.11 and made the default in Go 1.16, modules replace the older GOPATH approach with explicit dependency declarations, versioned releases, and a global proxy for faster, more reliable downloads.

## How Modules Work

A module is defined by a `go.mod` file at the root of your project. The module path typically matches the repository URL:

```go
module github.com/user/myproject

go 1.22

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/stretchr/testify v1.8.4
)
```

## Key Commands

```bash
go mod init github.com/user/myproject   # create go.mod
go get github.com/gin-gonic/gin        # add or update dependency
go get github.com/gin-gonic/gin@v1.9.0  # specific version
go mod tidy                             # add missing, remove unused
go mod download                          # download modules to cache
go mod verify                            # verify checksums
go mod graph                             # print dependency graph
go mod why -m github.com/pkg/errors     # explain why a module is needed
```

## Versioning

Go modules use semantic versioning with a convention for pre-release development:

```go
// Tagged releases (git tags)
go get github.com/foo/bar@v1.2.3

// Pre-release
go get github.com/foo/bar@v1.2.3-beta.1

// Pseudo-versions (for untagged commits)
go get github.com/foo/bar@v0.0.0-20240101000000-abc123def456

// Latest on a branch
go get github.com/foo/bar@main
```

### Major Versions

When a module reaches v2+, the module path includes the major version:

```go
// go.mod for v2
module github.com/user/myproject/v2
```

This allows v1 and v2 to coexist in the same dependency graph.

## The Go Proxy

By default, Go downloads modules from `proxy.golang.org` — a global read-through cache:

```bash
# The module proxy
GOPROXY=https://proxy.golang.org,direct

# Private modules (bypass proxy)
GOPROXY=proxy.golang.org
GONOSUMCHECK=github.com/myprivateorg/*
GONOSUMDB=github.com/myprivateorg/*
GOPRIVATE=github.com/myprivateorg/*
```

The proxy ensures:
- Modules never disappear (deleted tags are still served)
- Faster worldwide downloads (CDN-cached)
- Cryptographic verification via `go.sum`

## go.sum

The `go.sum` file contains cryptographic hashes for every module version used:

```
github.com/gin-gonic/gin v1.9.1 h1:abc...def
github.com/gin-gonic/gin v1.9.1/go.mod h1:hash...value
```

Go verifies every download against `go.sum`. If a hash doesn't match, the build fails. This provides supply chain security — tampered modules are detected immediately.

## Vendoring

Copy all dependencies into a `vendor/` directory within your project:

```bash
go mod vendor                    # create vendor directory
go build -mod=vendor             # build from vendor
```

Use vendoring when you need:
- Air-gapped builds (no network access)
- Full control over dependency code
- Code review of dependency changes

## Minimal Version Selection

Go uses **Minimal Version Selection (MVS)** — it picks the minimum version of each dependency that satisfies all requirements. Unlike npm's "latest compatible" approach, MVS is deterministic and never produces unexpected upgrades.

## Best Practices

- **Commit both `go.mod` and `go.sum`** — they're the source of truth for dependencies
- **Use `go mod tidy`** after adding or removing dependencies
- **Tag your releases** — consumers pin to tags, not branches
- **Run `go mod verify` in CI** — detect tampered or corrupted modules
- **Use `GONOSUMCHECK` for private modules** — skip hash verification for modules you control
- **Prefer the proxy** — don't set `GOPROXY=direct` unless you need to bypass it
- **Vendor only when necessary** — the proxy is faster and more reliable than vendoring
