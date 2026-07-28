# Other Ecosystems

> NuGet for .NET, Homebrew for macOS/Linux, and system package managers — dependency management beyond the major ecosystems.

> **Related:** [What Is a Package Manager?](what-is-a-package-manager.md) | [JavaScript Package Managers](javascript-package-managers.md)

---

## NuGet (.NET)

NuGet is the package manager for .NET (C#, F#, VB.NET). It's integrated into Visual Studio, Rider, and the `dotnet` CLI.

```bash
dotnet add package Newtonsoft.Json           # add a package
dotnet add package Serilog --version 3.1.1   # specific version
dotnet remove package Newtonsoft.Json        # remove
dotnet list package                          # list installed
dotnet list package --outdated               # check for updates
dotnet nuget locals all --clear              # clear cache
```

### Packages

Packages are published to **nuget.org**. Each package contains compiled `.dll` files, not source code.

```xml
<!-- .csproj file (or use dotnet CLI) -->
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
  <PackageReference Include="Serilog" Version="3.1.1" />
</ItemGroup>
```

### Versioning

NuGet supports several version formats:

| Format | Example | Meaning |
|--------|---------|---------|
| Exact | `13.0.3` | Only this version |
| Float | `13.0.*` | Latest patch |
| Range | `[13.0,14.0)` | >=13.0 and <14.0 |
| Wildcard | `*` | Latest |

### Private Feeds

Host private packages on Azure Artifacts, GitHub Packages, or a local NuGet server:

```xml
<configuration>
  <packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    <add key="MyPrivateFeed" value="https://pkgs.dev.azure.com/..." />
  </packageSources>
</configuration>
```

### NuGet Best Practices

- **Use `Directory.Packages.props`** — centralize package versions in multi-project solutions
- **Enable NuGet audit** — `dotnet list package --vulnerable` checks for known vulnerabilities
- **Pin versions** — avoid floating versions in production projects
- **Use lock files** — enable with `<RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>` in `.csproj`

## Homebrew

Homebrew is a package manager for macOS and Linux — it installs command-line tools, libraries, and applications.

```bash
brew install git         # install a formula
brew install --cask docker   # install a GUI app
brew update              # update Homebrew and formulae
brew upgrade             # upgrade all installed packages
brew outdated            # list outdated packages
brew search python       # search for a package
brew info python         # show package info
brew uninstall python    # uninstall
brew cleanup             # remove old versions
```

### Taps

Community or custom repositories (taps):

```bash
brew tap homebrew/cask-versions
brew tap myorg/mytap
```

### Brewfile

Reproduce a setup across machines:

```bash
# Generate Brewfile from installed packages
brew bundle dump

# Install from Brewfile
brew bundle
```

## System Package Managers

| OS | Manager | Common Use |
|----|---------|------------|
| Windows | winget | GUI apps, tools |
| Windows | Chocolatey | Legacy, enterprise |
| Windows | scoop | Command-line tools, portable |
| macOS | Homebrew | Everything |
| macOS | MacPorts | Open-source tools |
| Ubuntu/Debian | apt | System packages |
| Fedora/RHEL | dnf | System packages |
| Arch Linux | pacman | System packages |
| Alpine | apk | Minimal containers |

```bash
# winget (Windows)
winget install Microsoft.VisualStudioCode
winget upgrade --all

# apt (Ubuntu/Debian)
sudo apt update
sudo apt install python3
sudo apt upgrade

# pacman (Arch)
sudo pacman -S git
sudo pacman -Syu   # full system update
```

## Choosing by Language

```
Language   → Package Manager   → Primary Registry
─────────────────────────────────────────────
C#/.NET    → NuGet            → nuget.org
Ruby       → RubyGems         → rubygems.org
PHP        → Composer         → packagist.org
Julia      → Pkg.jl           → juliahub.com
Swift      → SwiftPM          → swiftpackageindex.com
Dart/Flutter → pub            → pub.dev
Elixir     → hex              → hex.pm
```
