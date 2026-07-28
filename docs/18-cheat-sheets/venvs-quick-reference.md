# Virtual Environments Quick Reference

> One-page reference for Python venv, conda, nvm, pyenv, and Node version management. Print this or bookmark it.

---

## Python venv

| Task | Command |
|------|---------|
| Create | `python -m venv .venv` |
| Activate (Win) | `.venv\Scripts\Activate.ps1` |
| Activate (Mac/Linux) | `source .venv/bin/activate` |
| Deactivate | `deactivate` |
| Freeze deps | `pip freeze > requirements.txt` |
| Install deps | `pip install -r requirements.txt` |
| Create from deps | `python -m venv .venv && pip install -r requirements.txt` |
| Remove | `Remove-Item -Recurse .venv` (Win) / `rm -rf .venv` (Mac/Linux) |

## conda

| Task | Command |
|------|---------|
| Create env | `conda create -n name python=3.12` |
| Activate | `conda activate name` |
| Deactivate | `conda deactivate` |
| List envs | `conda env list` |
| Remove env | `conda env remove -n name` |
| Export | `conda env export > env.yml` |
| Create from file | `conda env create -f env.yml` |
| Update all | `conda update --all` |
| Install package | `conda install pkg` |
| Search | `conda search pkg` |

## pyenv (Python Versions)

| Task | Command |
|------|---------|
| List versions | `pyenv versions` |
| List available | `pyenv install --list` |
| Install version | `pyenv install 3.12.0` |
| Set global | `pyenv global 3.12.0` |
| Set local | `pyenv local 3.12.0` |
| Set shell | `pyenv shell 3.12.0` |
| Uninstall | `pyenv uninstall 3.12.0` |

## Node Version Management

### nvm (Windows)

| Task | Command |
|------|---------|
| List installed | `nvm list` |
| List available | `nvm list available` |
| Install version | `nvm install 20` |
| Use version | `nvm use 20` |
| Uninstall | `nvm uninstall 20` |
| Default | `nvm alias default 20` |

### nvm (Mac/Linux)

| Task | Command |
|------|---------|
| List installed | `nvm ls` |
| List available | `nvm ls-remote --lts` |
| Install version | `nvm install 20` |
| Use version | `nvm use 20` |
| Uninstall | `nvm uninstall 20` |
| Default | `nvm alias default 20` |

### fnm (Fast Node Manager)

| Task | Command |
|------|---------|
| List installed | `fnm list` |
| List available | `fnm list-remote` |
| Install version | `fnm install 20` |
| Use version | `fnm use 20` |
| Default | `fnm default 20` |
| Current | `fnm current` |

## Version Files

| File | Purpose | Example |
|------|---------|---------|
| `.python-version` | pyenv/conda Python version | `3.12.0` |
| `.nvmrc` | nvm Node version | `20` |
| `.node-version` | fnm/nodenv Node version | `20` |
| `.tool-versions` | asdf multi-language | `python 3.12.0\nnodejs 20.0.0` |
| `runtime.txt` | Heroku Python version | `python-3.12.0` |
| `pyproject.toml` | Poetry/uv Python version | `requires-python = ">=3.12"` |

## Isolation Patterns

### Python: venv + pip (minimal)

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1    # Windows
pip install -r requirements.txt
```

### Python: venv + pip (dev tools)

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

### Python: Poetry (full lifecycle)

```bash
poetry new myproject
cd myproject
poetry add flask
poetry add -D pytest
poetry run pytest
poetry export -f requirements.txt -o requirements.txt
```

### Node: nvm + npm

```bash
nvm use 20
npm install
```

### Node: pnpm workspace

```bash
pnpm init
pnpm add -w typescript
pnpm -F "./packages/*" install
```

## Common Workflows

### Create Python project with venv

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install flask pytest
pip freeze > requirements.txt
```

### Switch Node versions per project

```bash
cd project-a
nvm use 18
cd ../project-b
nvm use 20
```

### Recreate Python env from scratch

```bash
Remove-Item -Recurse .venv
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Using system Python | Conflicts with OS packages | Always use venv |
| Committing `node_modules` | Bloat, conflicts | Add to `.gitignore` |
| Not committing lockfile | "Works on my machine" | Commit `package-lock.json` |
| Multiple Python versions without pyenv | Wrong version used | Use pyenv to manage versions |
| Using `sudo npm install` | Permission issues | Use nvm instead |
| Forgetting to activate venv | Installs to system | Always activate before pip install |

---

> **Full section:** [Virtual Environments](../08-virtual-environments/README.md) | **Next:** [AI Development](ai-dev-quick-reference.md)
