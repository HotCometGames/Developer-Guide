# asdf & Multi-Language Versioning

> A single tool for managing multiple language runtimes — Python, Node.js, Rust, and more.

> **Related:** [Python Version Management](python-version-management.md) | [Node Version Management](node-version-management.md)

---

## What Is It?

asdf is a unified version manager that handles multiple languages with a single CLI. Instead of installing pyenv for Python, nvm for Node, rustup for Rust, and gvm for Go, you install asdf once and use its plugin system for every language.

## Key Concepts

### .tool-versions

asdf uses a single `.tool-versions` file in your project root to declare all runtime versions:

```text
python 3.12.0
nodejs 22.0.0
rust 1.78.0
golang 1.22.0
```

This replaces: `.python-version`, `.nvmrc`, `.node-version`, `rust-toolchain.toml`.

### Plugin System

Each language is managed through a plugin:

```bash
asdf plugin add python          # add Python plugin
asdf plugin add nodejs          # add Node.js plugin
asdf plugin add rust            # add Rust plugin
asdf plugin list                # list installed plugins
asdf plugin list all            # list all available plugins
```

## Commands

```bash
asdf plugin add python                        # add a language plugin
asdf list all python                          # list installable versions
asdf install python 3.12.0                   # install a version
asdf install python latest:3                 # install latest Python 3.x
asdf current                                 # show current versions
asdf current python                          # show current Python version
asdf global python 3.12.0                    # set system-wide version
asdf local python 3.11.0                     # set per-project version
asdf list python                             # list installed versions
asdf uninstall python 3.11.0                 # remove a version
```

### Per-Project (.tool-versions)

```bash
cd myproject
asdf local python 3.12.0
asdf local nodejs 22.0.0
```

This creates `myproject/.tool-versions`. When you `cd` into the directory, asdf automatically sets the correct versions.

## How It Works

asdf uses **shims** — tiny wrapper scripts that intercept calls to `python`, `node`, `rustc`, etc. When you run `python`, asdf checks `.tool-versions` in the current directory (and parent directories), finds the requested version, and routes to the correct binary.

### Directory Hierarchy

asdf checks versions in this order:
1. `$PROJECT_ROOT/.tool-versions`
2. `$HOME/.tool-versions` (global)

## Comparison

| Feature | asdf | pyenv | nvm | fnm | rustup |
|---------|------|-------|-----|-----|--------|
| Languages | All (plugins) | Python only | Node only | Node only | Rust only |
| Single config | `.tool-versions` | `.python-version` | `.nvmrc` | `.nvmrc` | `rust-toolchain.toml` |
| Plugins | Yes | No | No | No | No |
| Speed | Moderate | Moderate | Moderate | Fast | Fast |
| Cross-platform | macOS, Linux | macOS, Linux, Win | Per-platform | All | All |

## When to Use asdf

**Use asdf when:**
- You work with 3+ languages regularly
- You want one config file (`.tool-versions`) instead of one per language
- You want a single command to install, update, and maintain version managers
- You're on macOS or Linux (Windows support exists via WSL)

**Use dedicated tools when:**
- You only need one or two languages
- You want the fastest possible tool (fnm for Node)
- You need Windows-native support (no WSL)

## Setup

```bash
# Install asdf (via git)
git clone https://github.com/asdf-vm/asdf.git ~/.asdf

# Add to shell profile
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
echo '. "$HOME/.asdf/completions/asdf.bash"' >> ~/.bashrc

# Restart shell, then install plugins
asdf plugin add python
asdf plugin add nodejs

# Install versions
asdf install python 3.12.0
asdf install nodejs 22.0.0
```

## Best Practices

- **Commit `.tool-versions`** — it tells every teammate exactly which versions to use
- **Use `asdf reshim`** after installing global packages (e.g., `npm install -g yarn` → `asdf reshim nodejs`)
- **Pin to patch versions** — `3.12.0` not `3.12` to ensure exact reproducibility
- **One `.tool-versions` per project** — don't use a global file for project-specific versions
- **Document asdf setup in CONTRIBUTING.md** — new contributors need the plugin install steps
