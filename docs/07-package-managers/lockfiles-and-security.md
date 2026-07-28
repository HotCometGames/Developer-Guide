# Lockfiles & Supply Chain Security

> How lockfiles enable deterministic builds and how to protect against supply chain attacks.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [JavaScript Package Managers](javascript-package-managers.md)

---

## What Is It?

Lockfiles pin dependency versions so every install produces the same result. Supply chain security is the practice of ensuring that the dependencies you install haven't been tampered with and don't contain known vulnerabilities.

## Why Lockfiles Matter

Without a lockfile, your build depends on when you last ran `install`:

```text
Day 1:  express@4.18.2 installed    (latest)
Day 30: express@4.19.0 installed    (latest — maybe breaking)
Day 60: express@4.20.0 installed    (maybe compromised)
```

With a lockfile, the same version is installed every time until you explicitly update.

### Lockfile Comparison by Ecosystem

| Ecosystem | Lockfile | CI Command |
|-----------|----------|------------|
| npm | `package-lock.json` | `npm ci` |
| yarn | `yarn.lock` | `yarn install --frozen-lockfile` |
| pnpm | `pnpm-lock.yaml` | `pnpm install --frozen-lockfile` |
| Python (pip) | No standard | `pip install -r requirements.txt` (manual pin) |
| Python (poetry) | `poetry.lock` | `poetry install --no-root` |
| Python (uv) | `uv.lock` | `uv sync --frozen` |
| Rust | `Cargo.lock` | `cargo build --locked` |
| Go | `go.sum` | `go build -mod=mod` |
| .NET | Packages lock file | `dotnet restore --locked-mode` |

## Deterministic Builds in CI

Always use the frozen/fixed install mode in CI:

```bash
# JavaScript
npm ci

# Rust
cargo build --locked

# Go
go build -mod=mod

# Python (uv)
uv sync --frozen
```

## Supply Chain Security Landscape

| Threat | Example | Impact |
|--------|---------|--------|
| Typosquatting | `requsts` instead of `requests` | Installs malicious package |
| Account compromise | Legitimate publisher's account stolen | Malicious update published |
| Dependency confusion | Public package with same name as private one | npm installs public (malicious) version |
| Embedded malware | Hidden code in build scripts | Data exfiltration, backdoors |
| Transitive dependency | A dependency's dependency is compromised | Indirectly affects your project |

## Defenses

### Audit Commands

```bash
# npm
npm audit                          # check for known vulnerabilities
npm audit --fix                    # auto-update to fix (may break things)

# yarn
yarn audit

# pnpm
pnpm audit

# Python
pip install pip-audit
pip-audit

# Rust
cargo install cargo-audit
cargo audit

# Go
govulncheck ./...

# .NET
dotnet list package --vulnerable
```

### Lockfile Signing & Verification

Some ecosystems verify package integrity:

| Mechanism | What It Does |
|-----------|-------------|
| npm registry signing | Packages can be signed by the publisher |
| Go `go.sum` | Cryptographic hash of every module version |
| Cargo `Cargo.lock` | Contains checksums, verified on build |
| PGP signatures | Optional for individual packages |
| Sigstore | Open-source signing (npm supports it) |

### CI Checks

Integrate security scanning into your CI pipeline:

```yaml
# GitHub Actions — Dependabot
- name: Dependabot
  uses: dependabot/dependabot-action@v2

# Third-party scanners
- name: Snyk
  uses: snyk/actions/node@master

- name: Trivy
  uses: aquasecurity/trivy-action@master
```

## Best Practices

- **Commit lockfiles** — never `.gitignore` a lockfile
- **Use frozen installs in CI** — fail the build if lockfile changes unexpectedly
- **Review lockfile diffs** — a lockfile change in a dependency-only PR should only change versions of intended packages
- **Pin exact versions where security matters** — lockfiles already do this, but check that ranges aren't too wide
- **Audit on every build** — integrate `npm audit` or equivalent into CI
- **Use private registries with caution** — vet and update mirrors regularly
- **Minimize dependency count** — fewer dependencies means smaller attack surface
- **Watch for deprecation warnings** — deprecated packages are often abandoned and become security risks
