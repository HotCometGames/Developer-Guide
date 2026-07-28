# Python Version Management

> Switching between Python versions with pyenv, uv, and conda.

> **Related:** [Python venv](python-venv.md) | [Conda Environments](conda-environments.md) | [Node Version Management](node-version-management.md)

---

## What Is It?

Python version managers let you install and switch between multiple Python versions on the same machine. They keep your system Python clean while giving each project the exact Python version it needs.

## The Problem

Your OS may ship with Python 3.9. But:
- Project A needs Python 3.11 (f-strings improvements, error messages)
- Project B needs Python 3.10 (library compatibility)
- You want to test your library against Python 3.9, 3.10, 3.11, and 3.12

A version manager solves this by installing multiple Python versions and switching between them per-directory or per-session.

## pyenv

pyenv installs and manages Python versions. It works by shimming `python` — you invoke `python` and pyenv intercepts the call to route to the correct version.

### Installation

```bash
# Windows (via pyenv-win)
git clone https://github.com/pyenv-win/pyenv-win.git ~/.pyenv

# macOS
brew install pyenv

# Linux
curl https://pyenv.run | bash
```

### Commands

```bash
pyenv install --list              # list available versions
pyenv install 3.12.0              # install a version
pyenv versions                    # list installed versions
pyenv global 3.12.0               # set system-wide Python
pyenv local 3.11.0                # set per-project (writes .python-version)
pyenv shell 3.10.0                # set for current shell session
```

### .python-version

When you run `pyenv local 3.11.0`, it writes a `.python-version` file:

```text
3.11.0
```

Commit this file — anyone with pyenv who runs `cd myproject` will automatically switch to the correct Python version.

### pyenv + venv

pyenv and venv work together perfectly:

```bash
pyenv local 3.12.0
python -m venv .venv          # uses pyenv's Python 3.12
.venv\Scripts\Activate.ps1    # or source .venv/bin/activate
```

## uv (Python + Version Management)

`uv` is a fast Python package and version manager in Rust. It replaces pip, venv, and pyenv in one tool.

```bash
uv python install 3.12.0       # install a Python version
uv python list                 # list installed versions
uv python pin 3.12.0           # set project version (writes .python-version)
uv venv                        # create venv using pinned version
```

uv reads `.python-version` (same format as pyenv), so you can standardize on one file format and let team members use either tool.

## Conda

Conda includes Python version management within each environment:

```bash
conda create -n myenv python=3.12
conda create -n legacy python=3.9
```

Conda environments are isolated from each other and can each run a different Python version. Unlike pyenv, you don't switch the global `python` — you activate the environment.

## Comparison

| Feature | pyenv | uv | Conda |
|---------|-------|-----|-------|
| Python versions | Many (any compiled version) | Many | Many |
| Non-Python packages | No | No | Yes |
| Works with venv | Yes | Built-in | Built-in |
| Speed | Moderate | Fast | Moderate |
| Global version switching | Yes | Yes | No (env-based) |
| Per-directory version | Yes (`.python-version`) | Yes (`.python-version`) | No |
| Platform | macOS, Linux, Windows | All | All |

## Best Practices

- **Commit `.python-version`** — lets teammates auto-switch versions
- **Use pyenv + venv** for most Python projects — simple, standard, widely understood
- **Use uv** if you want a single fast tool for everything
- **Use conda** when you also need non-Python packages
- **Don't modify the system Python** — let your OS manage it; use version managers for project work
