# VS Code Setup

> Installing, configuring, and customizing Visual Studio Code for development.

> **Related:** [VS Code Extensions](vs-code-extensions.md) | [Debugging](debugging.md)

---

## What Is It?

VS Code is a free, open-source code editor by Microsoft. It's the most popular editor in the world, with a rich extension ecosystem and deep language support.

## Installation

- **Windows:** Download from [code.visualstudio.com](https://code.visualstudio.com) or `winget install Microsoft.VisualStudioCode`
- **macOS:** `brew install --cask visual-studio-code`
- **Linux:** Download `.deb`/`.rpm` from the website or use your package manager

### CLI Setup

Enable the `code` command in your terminal:

- **Windows:** Check "Add to PATH" during install
- **macOS:** Run **Command Palette** → `Shell Command: Install 'code' command in PATH`
- **Linux:** Comes with the install

```bash
code .                # open current folder in VS Code
code file.txt         # open a file
code --diff a.txt b.txt   # diff two files
code --new-window .   # open in new window
```

## Essential Settings

Settings are stored in `settings.json`. Open it with **Ctrl+Shift+P** → `Preferences: Open Settings (JSON)`.

```json
{
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.minimap.enabled": false,
  "editor.wordWrap": "on",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "files.autoSave": "afterDelay",
  "workbench.colorTheme": "One Dark Pro",
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  "editor.cursorBlinking": "smooth",
  "explorer.confirmDelete": false,
  "files.exclude": {
    "**/__pycache__": true,
    "**/.git": true
  }
}
```

### Key Groups

| Category | Examples |
|----------|----------|
| Editor | `fontSize`, `tabSize`, `wordWrap`, `formatOnSave` |
| Files | `autoSave`, `exclude`, `encoding` |
| Workbench | `colorTheme`, `iconTheme`, `sideBar.location` |
| Terminal | `integrated.defaultProfile.*`, `integrated.fontSize` |
| Git | `git.enabled`, `git.autofetch`, `git.confirmSync` |

## Profiles

VS Code supports profiles for different workflows:

1. Open **File → Preferences → Profiles**
2. Create profiles like "Python Dev", "Game Dev", "Frontend"
3. Each profile has its own extensions, settings, and keybindings

Switch between profiles via the gear icon in the bottom-left.

## Keybindings

Customize in `keybindings.json` (**Ctrl+Shift+P** → `Preferences: Open Keyboard Shortcuts (JSON)`):

```json
[
  { "key": "ctrl+d", "command": "editor.action.copyLinesDownAction" },
  { "key": "ctrl+shift+d", "command": "editor.action.deleteLines" }
]
```

## Settings Sync

Sign in with GitHub or Microsoft to sync settings across machines:

1. Open **File → Preferences → Turn on Settings Sync**
2. Choose what to sync: settings, keybindings, extensions, UI state

## Command Line Power

```bash
code --install-extension ms-python.python     # install extension
code --list-extensions                        # list installed
code --uninstall-extension ms-python.python   # uninstall
code --status                                 # diagnostic info
```

## What's Next?

Browse [VS Code Extensions](vs-code-extensions.md) to find the right tools for your workflow.
