# Virtual Environments Troubleshooting

> Common virtual environment issues and how to fix them.

> **Related:** [Python venv](python-venv.md) | [Docker for Development](docker-for-development.md) | [Dev Containers](dev-containers.md)

---

## Python venv

### "Activate.ps1 cannot be loaded because running scripts is disabled on this system"

| Problem | Cause | Solution |
|---------|-------|----------|
| PowerShell execution policy blocks the script | Windows security policy | Run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` or use `.\venv\Scripts\python.exe` directly |

### "pip installs to system Python even after activating venv"

| Problem | Cause | Solution |
|---------|-------|----------|
| pip still uses system site-packages | The venv wasn't created with the correct Python, or `PIP_REQUIRE_VIRTUALENV` isn't set | Run `which python` / `Get-Command python` — it should point to `.venv/Scripts/python.exe`. If not, recreate the venv |

### "WARNING: You are using pip version X; however, version Y is available"

| Problem | Cause | Solution |
|---------|-------|----------|
| Old pip inside the venv | Newer venvs have old pip | Upgrade: `python -m pip install --upgrade pip`. Or create venv with `--upgrade-deps` |

### "The virtual environment was moved or copied and now it's broken"

| Problem | Cause | Solution |
|---------|-------|----------|
| Venv has absolute paths that are now wrong | Activating from a different location | Delete and recreate the venv — it's faster and more reliable than fixing it |

## Conda

### "CondaHTTPError: HTTP 000 CONNECTION FAILED"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't connect to conda channels | Network/proxy issue | Check proxy settings: `conda config --set proxy_servers.http http://proxy:port`. Or use `conda config --set ssl_verify false` (not recommended) |

### "Solving environment: failed with initial frozen solve. Retrying with flexible solve."

| Problem | Cause | Solution |
|---------|-------|----------|
| Package resolution is slow or failing | Complex dependency tree with incompatible versions | Use `conda config --set channel_priority strict`. Or create a fresh environment with minimal packages and add them one at a time |

### "Environment location is read-only"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't modify a conda environment | The environment is in a protected directory or you don't have write access | Use `conda create -p ./env` for a project-local environment (user-writable) |

## pyenv

### "pyenv: python: command not found" after install

| Problem | Cause | Solution |
|---------|-------|----------|
| Python version not activated | pyenv shims not in PATH | Run `pyenv rehash` or restart your shell. Ensure pyenv init is in your shell profile |

### "BUILD FAILED" when installing a Python version

| Problem | Cause | Solution |
|---------|-------|----------|
| Compilation fails | Missing build dependencies | Install build dependencies: `build-essential`, `libssl-dev`, `zlib1g-dev`, `libffi-dev` (Linux). On macOS, `brew install openssl readline sqlite3 xz zlib` |

## nvm / fnm

### "nvm is not compatible with the npm config prefix"

| Problem | Cause | Solution |
|---------|-------|----------|
| npm prefix conflicts with nvm | A global npm prefix is set | Remove the global prefix: `npm config delete prefix`. It conflicts with nvm's per-version approach |

### "nvm: command not found" after restarting terminal

| Problem | Cause | Solution |
|---------|-------|----------|
| nvm init not in shell profile | The shell profile wasn't updated | Add nvm to your shell profile: `export NVM_DIR="$HOME/.nvm"` and the nvm.sh source line. Restart |

## Docker

### "Bind: permission denied" when mounting volumes

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't access mounted files | File ownership mismatch between host and container | Ensure the host directory is shared in Docker Desktop settings. On Linux, use `:Z` flag for SELinux or run with `--user` matching your host UID |

### "docker compose up" is extremely slow

| Problem | Cause | Solution |
|---------|-------|----------|
| File sharing is slow | Windows/macOS file system virtualization overhead | Move the project into WSL2 (Windows) or use a Docker sync tool (mutagen). Avoid mounting entire directories with many files (`node_modules`) |

### "docker: command not found"

| Problem | Cause | Solution |
|---------|-------|----------|
| Docker not installed or not running | Docker Desktop isn't installed or the daemon isn't running | Install Docker Desktop. Ensure it's running (check the system tray icon) |

## Dev Containers

### "Failed to connect to the remote extension host server"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't connect to the Dev Container | Build failed or container crashed | Check the Dev Containers log: **Command Palette** → `Dev Containers: Show Log`. Look for build errors |

### "The container command 'yarn' could not be found"

| Problem | Cause | Solution |
|---------|-------|----------|
| A tool is missing | The base image or features didn't include it | Add the tool to the `postCreateCommand` or add a feature that includes it |

## General Diagnostics

| Problem | Approach |
|---------|----------|
| Python can't find installed packages | Check that you've activated the right environment: `which python` / `Get-Command python` |
| Node version is wrong | Run `node --version` and check `.nvmrc` / `.node-version` exists |
| Docker container exits immediately | Run `docker compose logs` to see the error. The CMD in the Dockerfile may be failing |
| "Works on my machine" but not in container | Compare the container's OS, Python version, and packages with your local environment |
| New terminal doesn't have the right environment | Ensure the activation command is in your shell profile, not just typed manually |
