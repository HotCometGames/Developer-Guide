# What Is a Virtual Environment?

> An isolated workspace that separates a project's dependencies and runtime from your system.

> **Related:** [Python venv](python-venv.md) | [Conda Environments](conda-environments.md) | [Docker for Development](docker-for-development.md)

---

## What Is It?

A virtual environment is a self-contained directory that holds a specific version of a language runtime and its installed packages. When you activate it, your shell uses that isolated environment instead of the system-wide installation.

## The Problem

Without virtual environments, all projects share the same global set of packages:

```text
System Python:    requests@2.30.0
Project A needs:  requests@2.28.0  (conflict!)
Project B needs:  requests@3.0.0   (also wants newer Python)
```

With virtual environments:

```text
Project A/.venv:  Python 3.11, requests@2.28.0
Project B/.venv:  Python 3.12, requests@3.0.0
System:           Python 3.10     (untouched by projects)
```

## What They Solve

| Problem | Without Isolation | With Isolation |
|---------|------------------|----------------|
| Version conflicts | Project A needs Flask 2, B needs Flask 3 | Each project has its own Flask version |
| System breakage | `pip install` upgrades a system package and something breaks | System packages are never touched |
| Reproducibility | "Works on my machine" | Lockfile + venv = identical environment |
| Clean uninstall | Uninstalling a project leaves stale packages everywhere | Delete the venv directory |
| Multiple Python versions | One Python on the system | Each project can use a different Python |

## Tools by Language

| Language | Environment Tools | Version Managers |
|----------|-----------------|-----------------|
| Python | venv, virtualenv, conda, poetry, uv | pyenv, uv |
| Node.js | npm (local node_modules) | nvm, fnm |
| Rust | cargo (per-project Cargo.lock) | rustup |
| Go | go modules (isolated by go.mod) | gvm |
| Multi-language | Docker, Dev Containers | asdf |

## The Isolation Spectrum

```
├── Venv/Python        ← Language-level isolation
├── nvm/Node           ← Runtime version switching
├── asdf               ← Multi-language version management
├── Docker             ← OS-level isolation
├── Dev Containers     ← Full development environment
└── Virtual Machine    ← Complete OS isolation
```

Each level adds more isolation but also more complexity. Choose the minimum level that solves your problem.

## Best Practices

- **Always use a virtual environment** — even for "small" projects
- **Keep the venv inside the project directory** — `.venv/` or `venv/` at the project root
- **Add `.venv/` to `.gitignore`** — never commit virtual environments
- **Commit the lockfile** — the environment definition, not the environment itself
- **Document the setup** — a `CONTRIBUTING.md` or Makefile with setup commands
- **Use consistent names** — `.venv/` is the convention across Python tools

## What's Next?

Start with [Python venv](python-venv.md) for Python projects, or jump to language-specific version management: [pyenv](python-version-management.md) or [nvm](node-version-management.md).
