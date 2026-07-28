# Python Package Managers

> pip, uv, poetry, and conda — managing Python packages and dependencies.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [Python venv](../08-virtual-environments/python-venv.md)

---

## What Is It?

Python's packaging landscape has historically been fragmented. In recent years, the ecosystem has converged around `pyproject.toml` as the standard configuration format, but multiple tools still compete for install and dependency management.

## The Options

### pip

The default package installer for Python. Minimal, simple, requires a separate tool for environment management.

```bash
pip install flask              # install package
pip install flask==3.0.0       # specific version
pip install -r requirements.txt # install from file
pip freeze > requirements.txt  # export pinned versions
pip list --outdated            # show outdated packages
pip show flask                 # package details
```

Best for: Simple projects, scripts, quick prototyping.

### uv

A Rust-based replacement for pip and venv — extremely fast, compatible with pip interfaces.

```bash
uv pip install flask            # pip-compatible interface
uv venv                         # create venv
uv pip compile pyproject.toml   # generate lockfile
uv pip sync requirements.txt    # fast sync from file
```

| Feature | pip | uv |
|---------|-----|----|
| Speed | Baseline | 10-100x faster |
| Venv management | Separate (`python -m venv`) | Built-in |
| Lockfile | Manual via `pip freeze` | `uv lock` |
| pip compatible | — | Yes (drop-in for most commands) |

Best for: Anyone who uses pip and wants it faster.

### poetry

A full-featured tool combining dependency management, packaging, and publishing.

```bash
poetry new myproject           # create new project
poetry add flask               # add dependency
poetry add --dev pytest        # dev dependency
poetry install                 # install from lockfile
poetry build                   # build package
poetry publish                 # publish to PyPI
poetry shell                   # activate virtual environment
```

```toml
# pyproject.toml
[tool.poetry]
name = "myproject"
version = "0.1.0"

[tool.poetry.dependencies]
python = ">=3.11"
flask = "^3.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

Best for: Projects that need publishing, teams wanting a unified tool.

### conda

Cross-language package manager popular in data science — handles Python, C libraries, and non-Python tools.

```bash
conda create -n myenv python=3.12
conda activate myenv
conda install numpy pandas
conda install -c conda-forge ffmpeg
conda env export > environment.yml
```

Best for: Data science, ML, projects with mixed-language dependencies.

## Comparison

| Feature | pip | uv | poetry | conda |
|---------|-----|----|--------|-------|
| Speed | Slow | Very fast | Medium | Medium |
| Lockfile | Manual | Built-in | Built-in | Built-in |
| Venv mgmt | Separate | Built-in | Built-in | Built-in |
| Non-Python deps | No | No | No | Yes |
| Publish to PyPI | No | No | Yes | No |
| pyproject.toml | Reads only | Reads only | Full | No |
| Complexity | Low | Low | Medium | Medium |

## Choosing the Right One

| Use Case | Recommendation |
|----------|---------------|
| Quick script, one-off | pip |
| Fast pip replacement | uv |
| Library or published package | poetry |
| Data science / ML | conda |
| Want all-in-one tool | poetry or conda |
| Speed-critical installs | uv |

## The Standard: pyproject.toml

Python has standardized on `pyproject.toml` for project configuration:

```toml
[build-system]
requires = ["setuptools>=68"]
build-backend = "setuptools.backends._legacy:_Backend"

[project]
name = "myproject"
version = "0.1.0"
requires-python = ">=3.11"
dependencies = [
    "flask>=3.0",
    "requests>=2.31",
]

[project.optional-dependencies]
dev = [
    "pytest>=8.0",
]
```

## Best Practices

- **Always use a virtual environment** — never `pip install` system-wide
- **Pin versions** — install from a lockfile or frozen requirements, not open ranges
- **Commit lockfiles** — ensure reproducible installs across environments
- **Use `pyproject.toml`** — it's the modern standard, not `setup.py`
- **Audit regularly** — `pip audit` or `pip-audit` for known vulnerabilities
