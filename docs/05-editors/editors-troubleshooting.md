# Editors Troubleshooting

> Common editor issues and how to fix them.

> **Related:** [VS Code Setup](vs-code-setup.md) | [Remote Development](remote-development.md)

---

## VS Code

### "Code is not recognized as an internal or external command"

| Problem | Cause | Solution |
|---------|-------|----------|
| `code` command not found | VS Code not added to PATH | Windows: Reinstall with "Add to PATH" checked. macOS: Run **Command Palette** → `Shell Command: Install 'code' command in PATH`. Linux: Reinstall or symlink `/usr/bin/code` |

### "Extensions not working" or "Extension host terminated unexpectedly"

| Problem | Cause | Solution |
|---------|-------|----------|
| Extensions crash | Corrupted extension data | Delete `~/.vscode/extensions` and reinstall. Or disable all extensions, enable one by one to find the culprit |
| GPU process crashed | Hardware acceleration issue | Add `"disable-hardware-acceleration": true` to VS Code settings or launch with `code --disable-gpu` |

### "Settings not syncing"

| Problem | Cause | Solution |
|---------|-------|----------|
| Settings Sync fails | Auth token expired or conflict | Sign out and back in via **File → Preferences → Turn off Settings Sync**, then re-enable |
| Conflict between machines | Different states on different devices | Turn on Settings Sync, choose "Merge" or "Replace" when prompted |

### "VS Code is slow or uses too much memory"

| Problem | Cause | Solution |
|---------|-------|----------|
| High memory usage | Too many extensions or large files | Disable unused extensions. For large files, try `"files.exclude"` or increase `"files.maxMemoryForLargeFilesMB"` |
| Slow startup | Many extensions load on startup | Review startup performance via **Help → Start Performance**. Disable slow extensions |

## Unity Editor

### "Scripts are not compiling"

| Problem | Cause | Solution |
|---------|-------|----------|
| Compilation errors | Syntax error in a script | Check the Console panel for error messages. Fix the error and wait for recompilation |
| Script is missing MonoBehaviour | Namespace or class name mismatch | Ensure the script inherits `MonoBehaviour` and the class name matches the filename |

### "The editor log is spamming errors"

| Problem | Cause | Solution |
|---------|-------|----------|
| Console full of errors | Null reference or missing component | Check the first error in the stack trace. Missing references or unassigned variables are the most common cause |

### "Build fails"

| Problem | Cause | Solution |
|---------|-------|----------|
| Build fails at 99% | Platform module not installed | Open **File → Build Profiles**, ensure the platform is installed via **Open Download Page** |
| Missing scenes in build | Scenes not added to build list | Add all required scenes to **Scenes in Build** in Build Profiles |

## Godot

### "GDScript errors on valid code"

| Problem | Cause | Solution |
|---------|-------|----------|
| False positive errors | Editor not fully loaded | Wait for the editor to finish parsing. Save and reload the script if errors persist |

### "Export templates not found"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't export project | Templates not installed | In editor: **Editor → Manage Export Templates...** → Download and install |

## Unreal Engine

### "Shader compilation too long"

| Problem | Cause | Solution |
|---------|-------|----------|
| Long load times | Shaders compiling on first launch | Allow compilation to finish. Subsequent launches are faster |
| "Infinite" shader compile | Complex materials or global illumination settings | Reduce material complexity, disable screen space reflections, or reduce shadow quality |

### "Blueprints not saving"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't save Blueprint | Compilation error in the graph | Check the **Compiler Results** panel for errors. Fix all errors and try saving again |

## General Editor Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Font is blurry or hard to read | Wrong font settings | Set `"editor.fontFamily": "Cascadia Code"` and `"editor.fontSize": 14`. Disable font ligatures if letters merge |
| Auto-format ruins my code | Formatter settings conflict | Ensure only one formatter is active (e.g., Prettier or black, not both). Set `"editor.formatOnSave": true` and check for conflicting formatter extensions |
| Git shows all files as changed (line endings) | CRLF/LF mismatch | Set `"files.eol": "\n"` in VS Code settings. Add `* text=auto` to `.gitattributes` |
