# Foundations Troubleshooting

> Common problems with paths, encoding, line endings, environment variables, ports, and the command prompt — and how to fix them.

> **Related:** [Environment Variables](environment-variables.md) | [Character Encoding](character-encoding.md) | [Line Endings](line-endings.md)

---

## "command not found" / "'xxx' is not recognized"

**Likely cause:** The tool's directory is not in your `PATH`.

**Fix:**
1. Find where the tool was installed (check install logs, try common locations like `C:\Program Files`, `/usr/local/bin`, `~/.local/bin`)
2. Add that directory to `PATH`:
   - **Windows:** System Properties → Environment Variables → Edit `PATH` → Add the directory
   - **Mac/Linux:** Add `export PATH="$PATH:/path/to/dir"` to `~/.zshrc` or `~/.bashrc`, then run `source ~/.zshrc`
3. Open a **new** terminal window (existing windows don't see the change)

**Prevention:** Most installers add themselves to PATH. If they don't, note the install path during installation.

---

## Files look correct but show as modified in git

**Likely cause:** Line ending mismatch (LF vs CRLF).

**Fix:**
```text
# Configure git properly
git config --global core.autocrlf true    # Windows
git config --global core.autocrlf input   # Mac/Linux

# Normalize the repo
git add --renormalize .
git commit -m "Normalize line endings"
```

**Prevention:** Add a `.gitattributes` file to your repository. See [Line Endings](line-endings.md) for the recommended template.

---

## "Port already in use" / Address already in use

**Likely cause:** Another process is already listening on that port.

**Fix:**
1. Find the process: `netstat -ano | findstr :3000` (Windows) or `lsof -i :3000` (Mac/Linux)
2. Kill it: `taskkill /PID <number>` (Windows) or `kill -9 <PID>` (Mac/Linux)
3. Or use a different port: `PORT=3001 npm start`

**Prevention:** Check port availability before starting a dev server. Use different ports for different projects.

---

## "Invalid byte sequence" / Garbled text / � characters

**Likely cause:** File is saved in one encoding but opened with another.

**Fix:**
1. Check the file's actual encoding: `file -I filename` (Mac/Linux) or check VS Code's bottom-right corner
2. Convert: `iconv -f latin1 -t utf8 input.txt > output.txt`
3. Or tell the tool what encoding to use: `open(file, encoding="utf-8")`

**Prevention:** Default to UTF-8 everywhere. Set your editor to save as UTF-8 by default.

---

## "Permission denied" when running a script

**Likely cause (Mac/Linux):** The file doesn't have execute permission.

**Fix:**
```bash
chmod +x script.sh
./script.sh
```

**Likely cause (Windows):** PowerShell execution policy or file is blocked.

**Fix:**
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Unblock-File script.ps1
```

**Prevention:** Make scripts executable as part of setup. Use `.sh` for scripts you'll run on Mac/Linux.

---

## The terminal says "no" or "not recognized" for basic commands

**Likely cause:** The `PATH` environment variable has been corrupted or is empty.

**Fix:**
```text
# Temporary fix — restore a basic PATH:
Windows:  set PATH=C:\Windows\System32;C:\Windows
Mac/Linux: export PATH=/usr/bin:/bin:/usr/sbin:/sbin

# Then fix your shell config file that corrupted it
```

**Prevention:** Never set `PATH=` (without appending) in your shell config. Always use `PATH="$PATH:/new/dir"`.

---

## "Empty reply from server" / Connection refused

**Likely cause:** The server isn't running, is running on a different port, or is bound to the wrong interface.

**Fix:**
1. Is the server running? Check with `ps aux | grep server` or `Get-Process -Name "server"`
2. Is it on the right port? Try `curl localhost:3000` — if that works but `localhost:3000` in browser doesn't, check the port
3. Is it bound to `localhost` or `0.0.0.0`? When starting: use `--host 0.0.0.0` to accept external connections
4. Is a firewall blocking it? Temporarily disable to test

**Prevention:** Always start with `localhost` (same machine). Use `0.0.0.0` only when other machines need to connect.

---

## Files show `^M` at the end of each line

**Likely cause:** You're viewing a Windows file (CRLF) on a Unix system.

**Fix:**
```bash
# Convert in place
dos2unix filename

# Or with sed
sed -i 's/\r$//' filename
```

**Prevention:** Configure Git's `core.autocrlf` setting (see [Line Endings](line-endings.md)).

---

## Git says "fatal: not a git repository" when you're in a project

**Likely cause:** You're in the wrong directory, or the `.git` folder was deleted.

**Fix:**
1. Run `pwd` to check where you are — you probably need to `cd` into the project root
2. If `.git` is missing, run `git init` to create a new repository, then connect to the remote again

**Prevention:** Check your current directory with `pwd` or the prompt before running git commands.

---

## "The file is being used by another process"

**Likely cause** (Windows): A program has the file open and won't release it.

**Fix:**
1. Close all programs that might be using the file
2. Use `handle.exe` (Sysinternals) or Resource Monitor to find what's locking it
3. Restart the computer if nothing else works

**Prevention:** Close files properly in code (use `with` blocks in Python, `using` blocks in C#).

---

## Related Topics

- [Environment Variables](environment-variables.md) — PATH troubleshooting details
- [Character Encoding](character-encoding.md) — More encoding fixes
- [Line Endings](line-endings.md) — More on CRLF/LF configuration
- [Networking Basics](networking-basics.md) — Port and connection troubleshooting

---

> **Next:** [Terminal](../02-terminal/README.md) | **Previous:** [The Command Prompt](the-command-prompt.md)
