# Remote Development

> Edit and debug code on remote servers, inside containers, and in cloud environments — all from your local editor.

> **Related:** [Editor Integrations](editor-integrations.md) | [Debugging](debugging.md)

---

## What Is It?

Remote development lets you run your editor's UI locally while the actual code, runtime, and tools live elsewhere. Your local editor feels like it's running remotely — full language support, debugging, and terminal — without any code on your machine.

## Remote SSH

Connect to a remote server via SSH and edit files as if they were local.

### Setup

1. Install the **Remote - SSH** extension in VS Code
2. Open the Command Palette (**Ctrl+Shift+P**) → `Remote-SSH: Connect to Host`
3. Enter `user@hostname` or `user@ip-address`
4. Select the config file (usually `~/.ssh/config`)

### SSH Config

```ssh-config
Host game-server
  HostName 192.168.1.100
  User ubuntu
  IdentityFile ~/.ssh/game-server-key
  ForwardAgent yes
```

Once connected, open any folder on the remote machine. All extensions run remotely, and the terminal connects directly to the remote server.

## Dev Containers

Develop inside a Docker container with a fully configured environment.

### Setup

1. Install the **Dev Containers** extension in VS Code
2. Open a folder → Command Palette → `Dev Containers: Reopen in Container`
3. Select or create a dev container configuration

### .devcontainer/devcontainer.json

```json
{
  "name": "Python 3",
  "image": "mcr.microsoft.com/devcontainers/python:3.12",
  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": ["ms-python.python", "ms-python.debugpy"],
      "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python"
      }
    }
  },
  "postCreateCommand": "pip install -r requirements.txt",
  "forwardPorts": [8000]
}
```

### Benefits

- **Consistent environment** — same tools for every team member
- **No local setup** — everything is in the container
- **Isolated** — different projects can have conflicting dependencies safely
- **Reproducible** — the config is committed to the repo

## GitHub Codespaces

Cloud-hosted dev environments that launch in your browser or VS Code.

### Setup

1. Open a repo on GitHub
2. Click **Code** → **Codespaces** → **Create codespace on main**
3. Configure via `.devcontainer/devcontainer.json`

### CLI

```bash
gh codespace create            # create a new codespace
gh codespace list              # list your codespaces
gh codespace code              # open in VS Code
gh codespace delete            # delete a codespace
```

| Feature | Codespaces | Dev Containers | Remote SSH |
|---------|-----------|---------------|------------|
| Where it runs | GitHub's cloud | Your machine | Your server |
| Setup time | Seconds | Minutes | Minutes |
| Cost | Free tier (120h/month) | Free | Server cost |
| Best for | Quick start, ephemeral work | Team consistency | Beefy on-prem hardware |

## Remote Debugging

All three methods support debugging with the same `launch.json` configuration. The debugger transparently connects to the remote runtime.

## Best Practices

- **Commit `.devcontainer` config** — makes onboarding instant
- **Use SSH keys** — avoid password prompts
- **Forward ports** — access remote servers (e.g., `localhost:3000` → remote dev server)
- **Install extensions locally** — UI extensions (themes) run locally; language extensions run remotely
- **Watch for latency** — some operations (like file save) may be slower over SSH
