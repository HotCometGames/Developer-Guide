# Python venv

> Python's built-in virtual environment system for isolating project dependencies.

> **Related:** [What Is a Virtual Environment?](what-is-a-virtual-environment.md) | [Conda Environments](conda-environments.md) | [Python Version Management](python-version-management.md)

---

## What Is It?

`venv` is Python's built-in module for creating lightweight virtual environments. It's included in Python 3.3+, needs no additional installation, and is the most widely used isolation tool in the Python ecosystem.

## Creating a Virtual Environment

```bash
python -m venv .venv
```

This creates a `.venv/` directory containing:
- `Scripts/` (Windows) or `bin/` (Linux/macOS) — Python executable and scripts
- `Lib/` or `lib/` — site-packages (where installed packages go)
- `pyvenv.cfg` — configuration pointing to the system Python

### Naming Convention

Always use `.venv` as the directory name:
- It's the community standard
- Tools like VS Code, `pre-commit`, and `pipenv` auto-detect it
- It's hidden (dot prefix) and conventional

## Activating and Deactivating

```bash
# Windows (PowerShell)
.venv\Scripts\Activate.ps1

# Windows (cmd)
.venv\Scripts\activate.bat

# macOS / Linux
source .venv/bin/activate

# Deactivate (any platform)
deactivate
```

When activated, the prompt changes to show `(.venv)` at the start. All `python` and `pip` commands now use the isolated environment.

## Working with Packages

```bash
# Inside the activated venv
pip install flask
pip install -r requirements.txt
pip list
pip freeze > requirements.txt
```

### requirements.txt

Pin exact versions for reproducibility:

```bash
pip freeze > requirements.txt
```

```text
flask==3.0.0
requests==2.31.0
gunicorn==22.0.0
```

Install from the file on a fresh clone:

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### requirements-dev.txt

Separate dev dependencies:

```text
-r requirements.txt
pytest==8.0.0
ruff==0.3.0
pre-commit==3.6.0
```

## Working with VS Code

VS Code auto-detects `.venv/` in the project root:

1. Open the project folder
2. Press **Ctrl+Shift+P** → `Python: Select Interpreter`
3. Choose `.venv\Scripts\python.exe`

VS Code remembers this per-project and automatically uses the correct interpreter for debugging, linting, and running code.

## Common Workflows

### Start a New Project

```bash
mkdir myproject && cd myproject
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install flask pytest
pip freeze > requirements.txt
```

### Clone and Set Up

```bash
git clone https://github.com/user/myproject.git
cd myproject
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### Reset the Environment

```bash
Remove-Item -Recurse .venv   # Windows
# or: rm -rf .venv            # macOS/Linux
python -m venv .venv
pip install -r requirements.txt
```

## Pitfalls

| Mistake | Why | Fix |
|---------|-----|-----|
| Forgetting to activate | Installs to system Python | Check prompt for `(.venv)`. Run `which python` to verify |
| Not committing `requirements.txt` | Can't recreate the environment | Run `pip freeze > requirements.txt` after installing |
| Committing `.venv/` | Bloat, platform-specific, conflicts | Add `.venv/` to `.gitignore` |
| Using `pip freeze` on system Python | Captures all global packages | Activate the venv first |
| Naming it `venv` instead of `.venv` | Less conventional, not hidden | Use `.venv/` — it's the standard |
