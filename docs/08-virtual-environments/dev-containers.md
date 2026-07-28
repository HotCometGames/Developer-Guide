# Dev Containers

> Fully configured development environments that run inside containers — opened directly in your editor.

> **Related:** [Docker for Development](docker-for-development.md) | [Remote Development](../05-editors/remote-development.md)

---

## What Is It?

A Dev Container is a Docker container configured as a full development environment. Your editor (VS Code, JetBrains) connects to the container and all language support, debugging, terminals, and extensions run inside it. The environment definition is committed to the repository — anyone who clones it gets the exact same setup with one click.

## How It Works

```text
┌──────────────────────────────────┐
│         Your Machine             │
│  ┌────────────────────────────┐  │
│  │    VS Code (UI only)       │  │
│  │    - File explorer         │  │
│  │    - Editor tabs           │  │
│  │    - Extensions (UI)       │  │
│  └──────────┬─────────────────┘  │
│             │ Remote connection   │
│  ┌──────────▼─────────────────┐  │
│  │    Docker Container        │  │
│  │    - Full OS + tools       │  │
│  │    - Language server       │  │
│  │    - Extensions (code)     │  │
│  │    - Terminal (in cont.)   │  │
│  │    - Debugger              │  │
│  │    - Your source code      │  │
│  └────────────────────────────┘  │
└──────────────────────────────────┘
```

## Configuration

### .devcontainer/devcontainer.json

```json
{
  "name": "Python 3.12 Dev",
  "image": "mcr.microsoft.com/devcontainers/python:3.12",

  "features": {
    "ghcr.io/devcontainers/features/docker-in-docker:2": {}
  },

  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "ms-python.debugpy",
        "charliermarsh.ruff"
      ],
      "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python",
        "python.terminal.activateEnvironment": true,
        "editor.formatOnSave": true
      }
    }
  },

  "postCreateCommand": "pip install -r requirements.txt",
  "forwardPorts": [8000],
  "remoteUser": "vscode"
}
```

### Using a Dockerfile

For more control, use a custom Dockerfile:

```json
{
  "name": "Custom Dev Container",
  "build": {
    "dockerfile": "Dockerfile",
    "context": ".."
  },
  "customizations": {
    "vscode": {
      "extensions": ["ms-python.python", "rust-lang.rust-analyzer"]
    }
  }
}
```

```dockerfile
# .devcontainer/Dockerfile
FROM mcr.microsoft.com/devcontainers/python:3.12

RUN apt-get update && apt-get install -y \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

RUN pip install poetry
```

## Opening a Dev Container

### VS Code

1. **Command Palette** → `Dev Containers: Reopen in Container`
2. VS Code builds the container and reconnects
3. You see "Dev Container: Python 3.12 Dev" in the bottom-left status bar

### VS Code CLI

```bash
code .                   # open locally
code --remote containers:project-name .   # open in container
```

### GitHub Codespaces

Dev Containers work with GitHub Codespaces — the same config powers both local and cloud development:

```bash
gh codespace create
gh codespace code
```

## Dev Container Features

Features are reusable, shareable configuration bundles maintained by the community:

| Feature | What It Adds |
|---------|-------------|
| `docker-in-docker` | Docker CLI inside the container |
| `git` | Git configuration |
| `github-cli` | `gh` CLI |
| `node` | Node.js + npm |
| `python` | Python + pip |
| `rust` | Rust + cargo |
| `terraform` | Terraform CLI |
| `aws-cli` | AWS CLI |

```json
{
  "features": {
    "ghcr.io/devcontainers/features/node:1": {
      "version": "22"
    },
    "ghcr.io/devcontainers/features/docker-in-docker:2": {}
  }
}
```

## Comparison

| Feature | Dev Containers | Docker Compose | venv / nvm |
|---------|---------------|----------------|------------|
| Editor integration | Full (extensions, debug, terminal) | Terminal only | Full (native) |
| Setup effort | Medium (write config) | Medium | Low |
| Reproducibility | Full (OS + tools + extensions) | Full (OS) | Language-level only |
| Multiple services | Via Docker Compose | Built-in | Manual |
| Team onboarding | One click | `docker compose up` | Multiple steps |
| Performance | Good (native on Linux) | Good | Best |
| Learning curve | Medium | Medium | Low |

## When to Use Dev Containers

**Use Dev Containers when:**
- You need a fully reproducible environment for the whole team
- Your project has complex system dependencies (C libraries, compilers, services)
- You want one-click onboarding for new contributors
- You use GitHub Codespaces

**Use simpler tools when:**
- Your project only needs language-level isolation
- You're working alone or on a small team
- You need maximum performance (Dev Containers add overhead)

## Best Practices

- **Commit `.devcontainer/` to the repo** — the config travels with the code
- **Keep devcontainer.json small** — use a Dockerfile for complex setup, devcontainer.json for config
- **Pin image versions** — `python:3.12` not `python:latest`
- **Use features sparingly** — each feature adds build time
- **Set up `postCreateCommand`** — auto-install dependencies after container creation
- **Forward ports for web services** — access `localhost:8000` when developing web apps
- **Add a `README.md` note** — tell contributors to "Reopen in Container" after cloning
