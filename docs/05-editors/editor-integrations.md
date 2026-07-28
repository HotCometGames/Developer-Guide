# Editor Integrations

> Connecting your editor to terminals, Git, task runners, and language servers for a seamless development workflow.

> **Related:** [VS Code Setup](vs-code-setup.md) | [Remote Development](remote-development.md)

---

## What Is It?

Modern editors aren't just for editing text. They integrate with the tools around your code — the terminal, version control, build systems, and language intelligence — so you spend less time switching windows and more time in flow.

## Integrated Terminal

VS Code, IntelliJ, Godot, and Unity all include an embedded terminal.

```bash
Ctrl+`                  # toggle terminal (VS Code)
```

| Feature | Benefit |
|---------|---------|
| Multiple terminals | Run dev server, tests, and build simultaneously |
| Split terminals | Watch output side by side |
| Custom shells | Set PowerShell, Bash, or WSL per workspace |
| Terminal tabs | Name and color-code terminals |

### VS Code Terminal Settings

```json
{
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  "terminal.integrated.fontSize": 13,
  "terminal.integrated.cursorBlinking": true,
  "terminal.integrated.scrollback": 10000
}
```

## Git Integration

Editors provide visual Git tools so you don't need the command line for common operations.

### VS Code

| Feature | How to Access |
|---------|--------------|
| View changes | Source Control view (**Ctrl+Shift+G**) |
| Stage/unstage | Click the + / - next to files |
| Commit | Type a message and press **Ctrl+Enter** |
| Branch switching | Click the branch name in the status bar |
| View diff | Click a changed file in the Source Control view |
| View blame | GitLens extension shows inline blame |
| Resolve conflicts | VS Code highlights conflict markers with GUI buttons |

### IntelliJ / Rider

- **Commit window** — **Ctrl+K**
- **Annotate** — right-click gutter → Annotate
- **Diff** — **Ctrl+D** on changed files

### Godot / Unity

- **Godot** — built-in Git control via the bottom panel
- **Unity** — integrates with external Git tools; no built-in Git UI

## Tasks & Build Automation

Automate common commands (build, test, lint) from within your editor.

### VS Code Tasks

Create `.vscode/tasks.json`:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run Tests",
      "type": "shell",
      "command": "pytest",
      "group": "test",
      "presentation": { "reveal": "always" }
    },
    {
      "label": "Build Site",
      "type": "shell",
      "command": "mkdocs build",
      "group": "build"
    }
  ]
}
```

Run a task: **Ctrl+Shift+P** → `Tasks: Run Task`.

### Godot

The built-in build system compiles GDScript/C# on save. Use the bottom panel for output.

### Unity

Use the Player Settings and Build Profiles in the editor window. External scripts are built through the IDE (Rider/VS).

## Language Server Protocol

LSP provides intelligent code features in your editor:

- **Go to definition** — **F12**
- **Find references** — **Shift+F12**
- **Hover for docs** — **Ctrl+K Ctrl+I**
- **Auto-complete** — appears as you type
- **Rename symbol** — **F2**
- **Code actions** — **Ctrl+.** (quick fixes, refactoring)

Most language extensions include an LSP server. If your editor supports LSP, you get IDE-level features for any language with an LSP server.

## Linting & Formatting on Save

Configure your editor to auto-format and lint when you save:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit",
    "source.organizeImports": "explicit"
  }
}
```

## What's Next?

Explore [Remote Development](remote-development.md) to use your editor with containers, remote servers, and cloud environments.
