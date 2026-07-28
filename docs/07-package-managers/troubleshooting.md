# Package Managers Troubleshooting

> Common package manager errors and how to fix them.

> **Related:** [Lockfiles & Supply Chain Security](lockfiles-and-security.md) | [Python Package Managers](python-package-managers.md)

---

## npm / yarn / pnpm

### "Module not found" after install

| Problem | Cause | Solution |
|---------|-------|----------|
| Package appears in `package.json` but not `node_modules` | Partial or corrupted install | Delete `node_modules` and lockfile, reinstall: `rm -rf node_modules && npm ci` |
| Can't find a locally installed binary | `node_modules/.bin` not in PATH | Use `npx` (npm), `yarn dlx` (yarn), or `pnpm dlx` (pnpm) |

### "Integrity check failed" or "Lockfile version mismatch"

| Problem | Cause | Solution |
|---------|-------|----------|
| Lockfile checksum mismatch | Corrupted download or lockfile edited manually | Delete `node_modules` and lockfile, reinstall. Never edit lockfiles manually |
| Different lockfile format | Team members using different npm/yarn/pnpm versions | Standardize the package manager version. Check `.npmrc` for registry changes |

### "EACCES: permission denied"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't write to global node_modules | Using `sudo npm install -g` | Use nvm to manage Node.js (no sudo needed). Or configure npm prefix to a user-owned directory |

### "npm ERR! code ENOENT" / "npm ERR! syscall rename"

| Problem | Cause | Solution |
|---------|-------|----------|
| File operations fail during install | Antivirus or file system lock | Retry the install. Disable real-time scanning temporarily. Clear npm cache: `npm cache clean --force` |

## pip / uv / poetry

### "No module named 'x'" despite `pip install x`

| Problem | Cause | Solution |
|---------|-------|----------|
| Package appears installed but import fails | Wrong Python environment | Check which Python you're using: `which python` / `Get-Command python`. Is your venv active? |
| Package installed in a different venv | Multiple virtual environments | Activate the correct venv: `source .venv/bin/activate` (Linux) or `.venv\Scripts\Activate.ps1` (Windows) |

### "ERROR: Could not find a version that satisfies the requirement x"

| Problem | Cause | Solution |
|---------|-------|----------|
| Package not found in PyPI | Wrong name or wrong index | Check the spelling. If it's a private package, add the index: `pip install --index-url https://...` |

### "Failed building wheel for x"

| Problem | Cause | Solution |
|---------|-------|----------|
| Package needs C extensions but can't build | Missing build tools (compiler, headers) | Install build tools: Windows: Build Tools for Visual Studio. Linux: `build-essential`, Python dev headers: `python3-dev` |

### "pip install freezes" or hangs

| Problem | Cause | Solution |
|---------|-------|----------|
| Resolution takes forever | Complex dependency tree with incompatible versions | Try `pip install --no-deps` then manually add deps. Or switch to `uv pip install` (faster resolver) |

## cargo

### "failed to select a version for 'x'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Dependency resolution fails | Conflicting version requirements from different crates | Check `cargo tree -i x` to see why both versions are needed. Update one of the dependents to use a compatible version |

### "Blocking waiting for file lock on package cache"

| Problem | Cause | Solution |
|---------|-------|----------|
| Cache locked by another instance | Another `cargo` process is running | Wait for it to finish, or kill the other process. Delete `~/.cargo/package-cache` if stale |

## go

### "missing go.sum entry" for module

| Problem | Cause | Solution |
|---------|-------|----------|
| `go.sum` is out of sync | `go.sum` doesn't include the module's checksum | Run `go mod tidy` to regenerate, then commit via `git add -A` |

### "go: inconsistent vendoring"

| Problem | Cause | Solution |
|---------|-------|----------|
| Vendor directory is out of date | Dependencies changed but vendor wasn't updated | Run `go mod vendor` again to refresh the vendor directory |

## NuGet

### "NU1107: Version conflict detected"

| Problem | Cause | Solution |
|---------|-------|----------|
| Two packages require different versions of the same dependency | Transitive conflict | Add a direct `PackageReference` to pin the version, or use `PackageReference Update` to force a version |

### "NU1301: Unable to load the service index for source"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't reach the NuGet feed | Network issue or wrong source URL | Check NuGet sources: `dotnet nuget list source`. Verify network connectivity |

## General Diagnostics

| Problem | Approach |
|---------|----------|
| Dependency conflict | Use `npm ls` / `cargo tree` / `go mod graph` / `dotnet list package` to see the full tree |
| Mysterious build failure | Delete lockfile and cache, reinstall fresh |
| "Works on my machine" | Compare lockfiles across environments. Ensure CI uses frozen-lockfile mode |
| Slow install | Switch to a faster package manager (uv, pnpm). Clear cache. Check network speed |
