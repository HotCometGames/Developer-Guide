# Cargo (Rust)

> Rust's package manager and build system — dependency management, builds, testing, and publishing.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [Lockfiles & Supply Chain Security](lockfiles-and-security.md)

---

## What Is It?

Cargo is Rust's integrated package manager and build system. Unlike npm or pip, Cargo handles both installing dependencies and compiling your code. It's the single entry point for most Rust project workflows.

## Key Features

### Project Scaffolding

```bash
cargo new myproject          # new binary project
cargo new --lib mylib        # new library project
cargo init                   # init in existing directory
```

Creates a standard structure:

```
myproject/
├── Cargo.toml
├── Cargo.lock
└── src/
    └── main.rs
```

### Dependency Management

Dependencies are declared in `Cargo.toml`:

```toml
[package]
name = "myproject"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1", features = ["full"] }
reqwest = "0.12"

[dev-dependencies]
criterion = "0.5"
```

### Version Resolution

Cargo resolves to the latest version within semver range at `cargo update`, then pins exact versions in `Cargo.lock`. Cargo uses **minimal version resolution** — it picks the minimum compatible version that satisfies all constraints.

```bash
cargo add serde              # add dependency
cargo add tokio --features full
cargo remove reqwest         # remove dependency
cargo update                 # update all dependencies
cargo update -p serde        # update a specific crate
```

### Build Commands

```bash
cargo build                  # debug build
cargo build --release        # optimized build
cargo check                  # type-check without producing binary (fast)
cargo run                    # build and run
cargo test                   # run tests
cargo bench                  # run benchmarks
cargo doc --open             # build and open docs
cargo clippy                 # run lints
cargo fmt                    # format code
```

### Workspaces

Cargo supports monorepos with workspaces:

```toml
# Root Cargo.toml
[workspace]
members = ["crates/*", "apps/api", "apps/cli"]
```

Each crate in the workspace shares a single `Cargo.lock` and build cache.

### Publishing

```bash
cargo login                  # authenticate with crates.io
cargo publish                # publish current crate
cargo owner --add github:myorg:my-team  # add owners
```

## Cargo.toml vs Cargo.lock

| File | Purpose | Commit? |
|------|---------|---------|
| `Cargo.toml` | Declares dependencies with version ranges | Yes |
| `Cargo.lock` | Exact resolved versions for all deps | Yes (for binaries), No (for libraries) |

For **applications**, commit `Cargo.lock` to ensure reproducible builds. For **libraries**, the lockfile is typically not committed — consumers resolve against their own lockfile.

## Features

Cargo features enable conditional compilation and optional dependencies:

```toml
[features]
default = ["full"]
full = ["serde", "tokio"]
web = ["reqwest"]
```

```rust
#[cfg(feature = "web")]
use reqwest;
```

Cargo resolves features across the dependency graph — if two crates request the same dependency with different features, Cargo merges them.

## Cargo Cache

Downloaded crates are cached at `~/.cargo/registry/` and `~/.cargo/git/`. Clear the cache with:

```bash
cargo cache --clear
```

## Best Practices

- **Commit Cargo.lock for applications** — ensures every build uses the same dependency versions
- **Use `cargo update -p <crate>`** to update specific dependencies, not a blanket `cargo update`
- **Pin the edition** — always specify `edition = "2021"` (or newer) in `Cargo.toml`
- **Use features sparingly** — too many features make the dependency graph complex
- **Audit with `cargo audit`** — `cargo install cargo-audit` then run `cargo audit` in CI
- **Run `cargo check` before `cargo build`** — faster iteration while developing
