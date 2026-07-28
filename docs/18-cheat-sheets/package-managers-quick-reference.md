# Package Managers Quick Reference

> One-page command reference for npm, yarn, pnpm, pip, poetry, cargo, and go mod. Print this or bookmark it.

---

## npm

| Task | Command |
|------|---------|
| Init | `npm init -y` |
| Install (all) | `npm install` |
| Install package | `npm install pkg` |
| Install dev | `npm install -D pkg` |
| Install global | `npm install -g pkg` |
| Uninstall | `npm uninstall pkg` |
| Update | `npm update` |
| Update one | `npm update pkg` |
| Outdated | `npm outdated` |
| Run script | `npm run name` |
| Exec binary | `npx pkg` |
| Search | `npm search term` |
| Info | `npm info pkg` |
| Version | `npm version patch` |
| Publish | `npm publish` |

## yarn

| Task | Command |
|------|---------|
| Init | `yarn init -y` |
| Install (all) | `yarn install` |
| Add package | `yarn add pkg` |
| Add dev | `yarn add -D pkg` |
| Add global | `yarn global add pkg` |
| Remove | `yarn remove pkg` |
| Update one | `yarn upgrade pkg` |
| Outdated | `yarn outdated` |
| Run script | `yarn run name` |
| Exec binary | `yarn dlx pkg` |
| Info | `yarn info pkg` |

## pnpm

| Task | Command |
|------|---------|
| Init | `pnpm init` |
| Install (all) | `pnpm install` |
| Add package | `pnpm add pkg` |
| Add dev | `pnpm add -D pkg` |
| Add global | `pnpm add -g pkg` |
| Remove | `pnpm remove pkg` |
| Update | `pnpm update` |
| Outdated | `pnpm outdated` |
| Run script | `pnpm run name` |
| Exec binary | `pnpm dlx pkg` |
| List | `pnpm list` |

## npm/yarn/pnpm Lockfiles

| Manager | Lockfile | Format |
|---------|----------|--------|
| npm | `package-lock.json` | JSON |
| yarn (v1) | `yarn.lock` | YAML-like |
| pnpm | `pnpm-lock.yaml` | YAML |

**Rule:** Never edit lockfiles manually. Always use the package manager.

## pip (Python)

| Task | Command |
|------|---------|
| Install | `pip install pkg` |
| Install version | `pip install pkg==1.0` |
| Install from file | `pip install -r requirements.txt` |
| Uninstall | `pip uninstall pkg` |
| List installed | `pip list` |
| Outdated | `pip list --outdated` |
| Freeze | `pip freeze` |
| Show info | `pip show pkg` |
| Search | `pip search term` |
| Download | `pip download pkg` |

## poetry (Python)

| Task | Command |
|------|---------|
| Init | `poetry init` |
| New project | `poetry new name` |
| Install (all) | `poetry install` |
| Add package | `poetry add pkg` |
| Add dev | `poetry add -D pkg` |
| Remove | `poetry remove pkg` |
| Update | `poetry update` |
| Show outdated | `poetry show --outdated` |
| Run command | `poetry run cmd` |
| Shell | `poetry shell` |
| Export | `poetry export -f requirements.txt` |
| Build | `poetry build` |
| Publish | `poetry publish` |

## cargo (Rust)

| Task | Command |
|------|---------|
| New project | `cargo new name` |
| Init | `cargo init` |
| Build | `cargo build` |
| Build release | `cargo build --release` |
| Run | `cargo run` |
| Check | `cargo check` |
| Test | `cargo test` |
| Add dependency | `cargo add pkg` |
| Add dev dep | `cargo add pkg --dev` |
| Remove dep | `cargo rm pkg` |
| Update deps | `cargo update` |
| Outdated | `cargo install cargo-outdated` |
| Doc | `cargo doc --open` |
| Publish | `cargo publish` |
| Bench | `cargo bench` |

## go mod (Go)

| Task | Command |
|------|---------|
| Init module | `go mod init path` |
| Download deps | `go mod download` |
| Add dependency | `go get pkg@version` |
| Tidy (clean) | `go mod tidy` |
| Vendor | `go mod vendor` |
| Show graph | `go mod graph` |
| Show why | `go mod why pkg` |
| Edit | `go mod edit` |
| Verify | `go mod verify` |

## Lockfiles & Registries

| Language | Lockfile | Registry | Config |
|----------|----------|----------|--------|
| JS/TS | `package-lock.json` | npmjs.com | `.npmrc` |
| JS/TS (yarn) | `yarn.lock` | npmjs.com | `.yarnrc` |
| JS/TS (pnpm) | `pnpm-lock.yaml` | npmjs.com | `.npmrc` |
| Python | — | pypi.org | `pyproject.toml` |
| Rust | `Cargo.lock` | crates.io | `Cargo.toml` |
| Go | `go.sum` | proxy.golang.org | `go.mod` |

## Common Workflows

### JS: Fresh install from lockfile

```bash
rm -rf node_modules
npm ci          # or: yarn --frozen-lockfile / pnpm install --frozen
```

### Python: Pin all versions

```bash
pip freeze > requirements.txt
# or with poetry:
poetry export -f requirements.txt --output requirements.txt
```

### Rust: Update one dependency

```bash
cargo update -p serde
```

### Go: Add specific version

```bash
go get github.com/pkg/errors@v0.9.0
go mod tidy
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Committing `node_modules` | Bloat, conflicts | Add to `.gitignore` |
| Editing lockfile | Corrupts dependency tree | Use package manager commands |
| Using `sudo npm install` | Permission mess | Fix permissions or use nvm |
| `pip install` without venv | System-wide pollution | Always use virtual environments |
| Ignoring lockfiles | "Works on my machine" | Commit lockfiles, use `--frozen` |

---

> **Full section:** [Package Managers](../07-package-managers/README.md) | **Next:** [Virtual Environments](venvs-quick-reference.md)
