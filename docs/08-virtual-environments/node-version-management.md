# Node Version Management

> Switching between Node.js versions with nvm, fnm, and version files.

> **Related:** [Python Version Management](python-version-management.md) | [asdf & Multi-Language Versioning](asdf.md)

---

## What Is It?

Node version managers let you install and switch between multiple Node.js versions. Different projects may require different Node versions (e.g., an old project on Node 16, a new one on Node 22), and the version manager handles the switching automatically.

## The Options

### nvm (Node Version Manager)

The original Node version manager. Available for both Windows and macOS/Linux.

**Windows:**

```bash
nvm list available              # list downloadable versions
nvm install 22                  # install latest Node 22
nvm install 20.11.0             # install specific version
nvm list                        # list installed versions
nvm use 22                      # use Node 22
nvm uninstall 20                # remove a version
nvm alias default 22            # set default version
```

**macOS/Linux:**

```bash
nvm ls-remote --lts             # list LTS versions
nvm install --lts               # install latest LTS
nvm install 20                  # install Node 20
nvm ls                          # list installed versions
nvm use 20                      # use Node 20
nvm alias default 22            # set default
```

### fnm (Fast Node Manager)

fnm is a Rust-based alternative to nvm — it's faster and works cross-platform.

```bash
fnm install 22                  # install Node 22
fnm list                        # list installed versions
fnm use 22                      # use Node 22
fnm current                     # show current version
fnm default 22                  # set default
fnm install --lts               # install latest LTS
```

fnm is the recommended option for new setups — faster and simpler than nvm.

## Version Files

Both nvm and fnm respect version files that tell them which Node version a project needs:

| File | Example | Tools |
|------|---------|-------|
| `.nvmrc` | `20` | nvm |
| `.node-version` | `20.11.0` | nvm, fnm, nodenv |
| `package.json` (engines) | `"node": ">=20"` | npm |

### .nvmrc

```bash
# .nvmrc
20
```

When you enter the project directory:

```bash
nvm use          # reads .nvmrc, switches automatically
fnm use          # reads .node-version or .nvmrc
```

### Auto-Switch (Shell Integration)

Add this to your shell profile for automatic version switching:

```bash
# fnm — automatic (recommended)
eval "$(fnm env --use-on-cd)"

# nvm — add to your shell profile
cd() { builtin cd "$@"; nvm use --silent 2>/dev/null; }
```

## Comparison

| Feature | nvm (Windows) | nvm (Mac/Linux) | fnm |
|---------|---------------|-----------------|-----|
| Speed | OK | OK | Fast (Rust) |
| Install Node | `nvm install 22` | `nvm install 22` | `fnm install 22` |
| Auto-switch | Manual | Shell hook | Built-in `--use-on-cd` |
| .nvmrc support | Yes | Yes | Yes |
| .node-version | No | No | Yes |
| Cross-platform | Windows only | Mac/Linux only | All |
| Popularity | Standard on Windows | Standard on Mac/Linux | Growing |

## Using the Correct Node Version

```bash
# Check current version
node --version

# Install project dependencies with the right Node
nvm use          # or fnm use
npm install

# Verify in CI
node --version   # should match .nvmrc
```

### Engines Field

Set the expected Node version in `package.json`:

```json
{
  "engines": {
    "node": ">=20.0.0",
    "npm": ">=10.0.0"
  }
}
```

Run `npm install` will warn if the engine doesn't match.

## Best Practices

- **Commit a version file** — `.nvmrc` or `.node-version` so the whole team uses the same Node
- **Use fnm for new setups** — it's faster and works the same across Windows, macOS, and Linux
- **Set a default version** — `nvm alias default 22` or `fnm default 22` for new projects
- **Pin the major version** — `.nvmrc` with `22` (not `22.11.0`) allows patch updates
- **Check engines in CI** — add `node --version` to your CI pipeline to verify the correct Node is used
