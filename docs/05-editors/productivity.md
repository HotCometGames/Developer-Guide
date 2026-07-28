# Productivity & Customization

> Editor features and habits that make you faster: multi-cursor, snippets, keybindings, and personalization.

> **Related:** [VS Code Setup](vs-code-setup.md) | [Editor Integrations](editor-integrations.md)

---

## What Is It?

Small editor habits compound into massive time savings. This page covers the features that separate fast developers from slow ones — multi-cursor editing, custom snippets, keybinding mastery, and intentional workspace customization.

## Multi-Cursor Editing

Edit multiple locations simultaneously:

| Shortcut | Action |
|----------|--------|
| `Alt+Click` | Add a cursor at click position |
| `Ctrl+Alt+Up/Down` | Add cursor above/below |
| `Ctrl+D` | Select next occurrence of the current word |
| `Ctrl+Shift+L` | Select all occurrences |
| `Alt+Shift+I` | Add cursor at end of each selected line |
| `Shift+Alt+drag` | Column (box) selection |

### Real-World Examples

**Rename a variable in scope:** Click the variable name → `Ctrl+D` repeatedly → type the new name.

**Add a suffix to multiple lines:** Select the lines → `Alt+Shift+I` → type the suffix.

**Edit a list:** Column-select the first character of each line → type the change.

## Snippets

Snippets are shortcuts that expand into common code patterns.

### Built-in Snippets

Many languages include built-in snippets:

| Trigger | Expands To |
|---------|-----------|
| `for` in JavaScript | `for (let index = 0; index < array.length; index++) { ... }` |
| `class` in Python | A class definition template |
| `fn` in Rust | A function declaration |

### Custom Snippets

Create your own in `.vscode/*.code-snippets` or via **File → Preferences → Configure User Snippets**:

```json
{
  "Python Debug": {
    "prefix": "pdb",
    "scope": "python",
    "body": [
      "import pdb; pdb.set_trace()  # ${1:debug}"
    ],
    "description": "Insert pdb breakpoint"
  },
  "Console Log": {
    "prefix": "clog",
    "scope": "javascript,typescript",
    "body": "console.log('${1:var}:', ${1:var});",
    "description": "Log a variable"
  }
}
```

Use placeholders (`${1:default}`) to tab through fill-in fields.

## Keybindings That Matter

Learn these platform-agnostic patterns:

| Habit | Why It Matters |
|-------|---------------|
| **Ctrl+P** → type filename | Never use the file tree to navigate |
| **Ctrl+Shift+P** → type command | Everything is a command |
| **Ctrl+D** → select next occurrence | Edit faster than find-and-replace |
| **Ctrl+G** → line number | Jump to the exact line from an error |
| **Ctrl+\`** → toggle terminal | Stay in flow |
| **Ctrl+B** → toggle sidebar | More screen space when reading |
| **Ctrl+Shift+K** → delete line | Faster than selecting + deleting |
| **Alt+Up/Down** → move line | Rearrange code without cut-paste |

## Themes & Visual Customization

Your editor should be comfortable for 8+ hours a day.

### Choosing a Theme

- **High contrast** for bright rooms or accessibility
- **Low contrast** for dark rooms, late nights
- **Consistent colors** — syntax highlighting should be readable, not pretty

### Recommended

| Theme | Vibe |
|-------|------|
| One Dark Pro | Balanced, most popular |
| Dracula | High contrast, vibrant |
| Tokyo Night | Muted, easy on the eyes |
| GitHub Light Default | Clean, familiar for web devs |
| Catppuccin | Soft pastels, low eyestrain |

### Fonts

Programming fonts have distinct characters (zero with dot, l/1 distinction):

- **Cascadia Code** — Microsoft's font with ligatures
- **JetBrains Mono** — designed for IDEs
- **Fira Code** — popular with ligatures
- **Victor Mono** — cursive italics

```json
{
  "editor.fontFamily": "JetBrains Mono, Cascadia Code, monospace",
  "editor.fontLigatures": true,
  "editor.fontSize": 14
}
```

## Customizing the Workspace

```json
{
  "workbench.colorTheme": "Tokyo Night",
  "workbench.iconTheme": "material-icon-theme",
  "editor.minimap.enabled": false,
  "workbench.startupEditor": "none",
  "window.zoomLevel": 0,
  "editor.renderWhitespace": "boundary",
  "editor.rulers": [80, 100]
}
```

## Building Habits

- **Learn one shortcut per day** — try it until it's automatic
- **Don't use the mouse for navigation** — force yourself to use Ctrl+P, Ctrl+Tab, Ctrl+G
- **Customize as you go** — when you repeat an action 3 times, make it a snippet or keybinding
- **Watch other developers** — you'll pick up habits you didn't know existed
