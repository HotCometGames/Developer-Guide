# Editors Quick Reference

> One-page keyboard shortcut reference for VS Code and Neovim. Print this or bookmark it.

---

## VS Code — Essential Shortcuts

### Navigation

| Shortcut | Action |
|----------|--------|
| `Ctrl+P` | Quick open file |
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+G` | Go to line |
| `Ctrl+Shift+O` | Go to symbol |
| `Ctrl+T` | Go to symbol in workspace |
| `Alt+Left/Right` | Navigate back/forward |
| `Ctrl+Tab` | Switch between editors |
| `Ctrl+1/2/3` | Focus editor group 1/2/3 |
| `Ctrl+B` | Toggle sidebar |
| `Ctrl+J` | Toggle panel |
| `` Ctrl+` `` | Toggle terminal |

### Editing

| Shortcut | Action |
|----------|--------|
| `Ctrl+D` | Select next occurrence |
| `Ctrl+Shift+L` | Select all occurrences |
| `Alt+Up/Down` | Move line up/down |
| `Shift+Alt+Up/Down` | Copy line up/down |
| `Ctrl+Shift+K` | Delete line |
| `Ctrl+/` | Toggle comment |
| `Shift+Alt+A` | Toggle block comment |
| `Ctrl+Shift+F` | Find in files |
| `Ctrl+H` | Find and replace |
| `Ctrl+Space` | Trigger suggest |
| `Ctrl+Shift+Space` | Trigger parameter hints |
| `F2` | Rename symbol |
| `Ctrl+.` | Quick fix |
| `Shift+Alt+F` | Format document |

### Selection & Multi-Cursor

| Shortcut | Action |
|----------|--------|
| `Alt+Click` | Add cursor |
| `Ctrl+Alt+Up/Down` | Add cursor above/below |
| `Ctrl+Shift+L` | Select all occurrences |
| `Ctrl+Shift+Right` | Expand selection |
| `Ctrl+Shift+Left` | Shrink selection |
| `Alt+Shift+I` | Add cursor at line ends |

### Files & Windows

| Shortcut | Action |
|----------|--------|
| `Ctrl+N` | New file |
| `Ctrl+S` | Save |
| `Ctrl+Shift+S` | Save as |
| `Ctrl+W` | Close editor |
| `Ctrl+K W` | Close all editors |
| `Ctrl+\` | Split editor |
| `Ctrl+K Ctrl+O` | Open folder |

### Git (built-in)

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+G` | Source control view |
| `Ctrl+K Ctrl+G` | Git: commit |
| `Ctrl+K R` | Open in remote |

## VS Code — Useful Settings

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
  "terminal.integrated.defaultProfile.windows": "PowerShell"
}
```

## VS Code — Essential Extensions

| Extension | Purpose |
|-----------|---------|
| Prettier | Code formatting |
| ESLint | JS/TS linting |
| GitLens | Git blame & history |
| Error Lens | Inline errors |
| Thunder Client | API testing |
| Remote SSH | Edit remote files |
| Python | Python support |
| rust-analyzer | Rust support |

## Neovim — Modes

| Mode | Purpose | Enter from Normal |
|------|---------|-------------------|
| Normal | Navigation & commands | `Esc` |
| Insert | Typing text | `i`, `a`, `o`, `I`, `A`, `O` |
| Visual | Selection | `v`, `V`, `Ctrl+V` |
| Command | Ex commands | `:` |

## Neovim — Essential Commands

### Navigation

| Command | Action |
|---------|--------|
| `h j k l` | Left/down/up/right |
| `w` / `b` | Next/previous word |
| `0` / `$` | Start/end of line |
| `gg` / `G` | Top/bottom of file |
| `Ctrl+D` / `Ctrl+U` | Half page down/up |
| `H` / `M` / `L` | Top/middle/bottom of screen |
| `%` | Matching bracket |
| `f{char}` | Jump to char forward |
| `;` / `,` | Repeat f/F/t/T forward/back |

### Editing

| Command | Action |
|---------|--------|
| `i` / `a` | Insert before/after cursor |
| `I` / `A` | Insert at start/end of line |
| `o` / `O` | New line below/above |
| `x` | Delete char |
| `dd` | Delete line |
| `D` | Delete to end of line |
| `dw` | Delete word |
| `yy` | Yank (copy) line |
| `yw` | Yank word |
| `p` / `P` | Paste after/before |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last change |

### Search & Replace

| Command | Action |
|---------|--------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` / `N` | Next/previous match |
| `:%s/old/new/g` | Replace all in file |
| `:s/old/new/g` | Replace all in selection |

### Files & Splits

| Command | Action |
|---------|--------|
| `:e file` | Open file |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `:sp` | Horizontal split |
| `:vsp` | Vertical split |
| `Ctrl+w h/j/k/l` | Navigate splits |
| `:bn` / `:bp` | Next/previous buffer |
| `:bd` | Close buffer |

### Treesitter & LSP (with plugins)

| Command | Action |
|---------|--------|
| `gd` | Go to definition |
| `gr` | Find references |
| `K` | Hover documentation |
| `Ctrl+k Ctrl+d` | Jump to declaration |
| `<leader>rn` | Rename symbol |
| `<leader>ca` | Code action |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Using arrow keys in Neovim | Breaks muscle memory | Use `hjkl` |
| Saving in Neovim insert mode | Leaves insert mode | Use `Esc` then `:w` |
| Not using `Ctrl+P` in VS Code | Slow file navigation | Use `Ctrl+P` for instant access |
| Ignoring multi-cursor | Manual repetition | Use `Ctrl+D` to select all occurrences |

---

> **Full section:** [Editors](../05-editors/README.md) | **Next:** [Virtual Environments](venvs-quick-reference.md)
