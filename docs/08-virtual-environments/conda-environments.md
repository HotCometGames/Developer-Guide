# Conda Environments

> Conda's cross-language package and environment manager, popular in data science and ML.

> **Related:** [Python venv](python-venv.md) | [What Is a Virtual Environment?](what-is-a-virtual-environment.md) | [Python Version Management](python-version-management.md)

---

## What Is It?

Conda is an open-source package and environment manager that works across languages. Unlike venv, Conda can install non-Python dependencies (C libraries, CUDA, R packages) and manage different Python versions within each environment.

## Creating Environments

```bash
conda create -n myenv python=3.12       # create with Python
conda create -n myenv python=3.12 numpy pandas  # create with packages
conda env create -f environment.yml      # create from file
```

| Flag | Meaning |
|------|---------|
| `-n myenv` | Environment name |
| `-p ./path/env` | Environment at a specific path (project-local) |
| `-f environment.yml` | Create from exported file |

## Activation

```bash
conda activate myenv
conda deactivate            # exit current env
conda activate ./env        # activate project-local env
```

## Installing Packages

```bash
conda install numpy                # install from defaults channel
conda install -c conda-forge ffmpeg  # install from conda-forge
conda install pip                   # pip works inside conda
pip install flask                  # use pip for packages not in conda
```

### Channels

Channels are Conda's equivalent of registries:

```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
```

| Channel | Content |
|---------|---------|
| `defaults` | Anaconda's curated packages |
| `conda-forge` | Community-maintained, most packages (recommended) |
| `bioconda` | Bioinformatics software |
| `pytorch` | PyTorch releases |
| `nvidia` | CUDA tools |

## Managing Environments

```bash
conda env list                  # list all environments
conda list                      # list packages in current env
conda list -n myenv             # list packages in specific env
conda remove -n myenv --all     # delete an environment
```

## Exporting and Sharing

```yaml
# environment.yml
name: myenv
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.12
  - numpy>=1.26
  - pandas>=2.1
  - pip
  - pip:
    - flask==3.0.0
```

```bash
conda env export > environment.yml     # exact export (platform-specific)
conda env export --from-history > environment.yml  # only explicitly-installed
conda env create -f environment.yml    # recreate from file
```

## Conda vs venv

| Aspect | venv | Conda |
|--------|------|-------|
| Included with | Python 3.3+ | Must install (Miniconda/Anaconda) |
| Scope | Python only | Multi-language (R, C, CUDA) |
| Non-python packages | No | Yes (ffmpeg, CUDA, compilers) |
| Python version | Inherits from system | Any version in the environment |
| Package sources | PyPI only | Conda channels + PyPI |
| Lockfile | Manual (`requirements.txt`) | `conda env export` |
| Environment location | Project directory (`./.venv`) | Centralized by default (`~/anaconda3/envs/`) |
| Binary packages | Wheels (pip) | Pre-built binaries (conda) |
| Speed | Fast | Slower resolution, bigger downloads |

## When to Use Conda

**Use conda when:**
- You need non-Python dependencies (CUDA, libraries, compilers)
- You're doing data science or machine learning
- Different projects need different Python versions
- You want a single tool for packages + environments

**Use venv when:**
- You only need Python packages
- You want the simplest, most standard setup
- You're building a web app or script
- You want project-local environments (not centralized)

## MiniConda vs Anaconda

| Distribution | Size | Includes |
|-------------|------|----------|
| Miniconda | ~80 MB | Conda + Python + essential tools |
| Anaconda | ~3 GB | Conda + Python + 250+ pre-installed packages |

Start with **Miniconda** — install only what you need.

## Best Practices

- **Prefer `conda-forge`** — set it as the default channel
- **Use `--from-history` for export** — produces cleaner, platform-agnostic environment files
- **Don't mix conda and pip without care** — install conda packages first, then pip
- **Use project-local environments** — `conda create -p ./env python=3.12` for per-project isolation
- **Keep base env clean** — don't install project packages in the base environment
