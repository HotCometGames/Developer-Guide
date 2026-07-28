# Debugging

> Using debuggers to step through code, inspect variables, and find bugs.

> **Related:** [VS Code Setup](vs-code-setup.md) | [Editor Integrations](editor-integrations.md)

---

## What Is It?

Debugging is the process of running your code in a controlled environment where you can pause execution, inspect state, and step through logic line by line. VS Code includes a built-in debugger that works with most languages.

## Core Concepts

| Concept | What It Is |
|---------|------------|
| Breakpoint | A marker where execution pauses |
| Step Over | Execute the current line, then pause at the next |
| Step Into | Enter a function call to debug inside it |
| Step Out | Finish the current function and return to the caller |
| Watch | Track the value of a specific variable or expression |
| Call Stack | The chain of function calls that led to the current point |
| Debug Console | A REPL that runs in the current execution context |

## Setting Breakpoints

Click the gutter (left of the line number) to add a breakpoint. VS Code shows a red dot.

**Types of breakpoints:**

| Type | How | Use Case |
|------|-----|----------|
| Line breakpoint | Click gutter | Pause at a specific line |
| Conditional breakpoint | Right-click gutter → Add conditional | Pause when a condition is true |
| Hit count breakpoint | Right-click → Hit count | Pause after N hits |
| Logpoint | Right-click → Add logpoint | Log a message without stopping |
| Exception breakpoint | Debug view → Breakpoints | Pause on thrown/caught exceptions |

## Launch Configurations

Create a `.vscode/launch.json` file to configure debugging:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "debugpy",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    },
    {
      "name": "Node.js: Attach",
      "type": "node",
      "request": "attach",
      "port": 9229
    }
  ]
}
```

### Common Launch Types

| Request | What It Does |
|---------|-------------|
| `launch` | VS Code starts the program |
| `attach` | VS Code connects to an already-running process |

## Debugging Workflow

1. Set breakpoints in your code
2. Press **F5** to start debugging
3. Use the debug toolbar to step through:
   - **Continue (F5)** — run to next breakpoint
   - **Step Over (F10)** — execute line, stay in current function
   - **Step Into (F11)** — enter function calls
   - **Step Out (Shift+F11)** — finish function and return
   - **Restart (Ctrl+Shift+F5)** — restart debugging
   - **Stop (Shift+F5)** — end debugging session
4. Hover over variables to see their values
5. Add expressions to the Watch panel

## Debug Console

Use the Debug Console to evaluate expressions while paused:

```
> myVariable
> len(items)
> user.name.upper()
> [x for x in range(10)]
```

The console runs in the current scope and can modify variables.

## Inspecting State

| Panel | What It Shows |
|-------|-------------|
| Variables | Local, global, and closure variables |
| Watch | Custom expressions you've added |
| Call Stack | The chain of function calls |
| Loaded Scripts | All scripts loaded in the runtime |
| Breakpoints | All breakpoints with enabled/disabled state |

## Multi-Target Debugging

Debug both a frontend and backend simultaneously:

```json
{
  "configurations": [
    { "name": "Backend", ... },
    { "name": "Frontend", ... }
  ],
  "compounds": [
    {
      "name": "Full App",
      "configurations": ["Backend", "Frontend"]
    }
  ]
}
```

## Remote Debugging

### Attach to a Remote Process

For Node.js:

```bash
node --inspect=0.0.0.0:9229 app.js
```

Then use an "Attach" launch configuration in VS Code.

### Dev Containers

Debug inside a container with the same `launch.json` — the debugger transparently connects to the container runtime.

## Common Debugging Tips

- **Use conditional breakpoints** instead of scrolling to find the right iteration
- **Logpoints** are great for production issues where you can't stop execution
- **Check the call stack** when you don't know how you reached a line
- **Restart between runs** — stale state causes confusing bugs
- **Simplify** — if debugging is hard, reduce the test case to the minimum
