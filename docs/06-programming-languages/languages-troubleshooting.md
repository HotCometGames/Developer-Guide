# Programming Languages Troubleshooting

> Common errors by language and how to diagnose them.

> **Related:** [Python](python.md) | [JavaScript](javascript.md) | [TypeScript](typescript.md) | [C#](csharp.md) | [C++](cpp.md) | [SQL](sql.md)

---

## Python

### "ModuleNotFoundError: No module named 'x'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Import fails | Package not installed or not in the right environment | `pip install x` or check which venv is active: `which python` / `Get-Command python` |

### "NameError: name 'x' is not defined"

| Problem | Cause | Solution |
|---------|-------|----------|
| Variable not found | Typo, scope issue, or variable used before assignment | Check spelling. Is the variable inside a function but used outside? Is the assignment after usage? |

### "TypeError: 'int' object is not callable"

| Problem | Cause | Solution |
|---------|-------|----------|
| Trying to call a number as a function | You reused a function name as a variable | `sum = 10` then later `sum([1,2,3])` — don't shadow built-in names |

### "IndentationError: unexpected indent"

| Problem | Cause | Solution |
|---------|-------|----------|
| Inconsistent indentation | Mixing tabs and spaces, or wrong indent level | Use `ruff format` or `black` to auto-fix. Configure your editor to use spaces for Python |

## JavaScript

### "Cannot read properties of undefined (reading 'x')"

| Problem | Cause | Solution |
|---------|-------|----------|
| Accessing a property on `undefined` | A variable or object property is `undefined` | Check if the value exists before accessing: `obj?.prop` (optional chaining) |

### "x is not a function"

| Problem | Cause | Solution |
|---------|-------|----------|
| Calling a non-function value | Variable name collision or wrong import | Check if the variable is a function or something else. Look for `typeof x` |

### "Unexpected token 'export'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Can't use ES modules | Using `import`/`export` in CommonJS context | Add `"type": "module"` to `package.json` or rename file to `.mjs` |

### "ReferenceError: x is not defined" (with let/const)

| Problem | Cause | Solution |
|---------|-------|----------|
| Temporal dead zone | Using `let`/`const` before declaration | Move the reference after the declaration. `let` and `const` are not hoisted like `var` |

## TypeScript

### "Type 'undefined' is not assignable to type 'X'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Value might be undefined | Strict null checks enabled | Handle the undefined case: `if (x !== undefined) { ... }` or use `x!` if you know it's defined |

### "Property 'x' does not exist on type 'Y'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Accessing a property not on the type | Wrong type, missing property, or need narrowing | Add the property to the type, narrow the type, or use type assertion |

### "This expression is not callable"

| Problem | Cause | Solution |
|---------|-------|----------|
| Calling something that isn't a function | Union type includes a non-function variant | Narrow the type before calling. Type guard or `typeof` check |

### "Cannot find module 'x' or its corresponding type declarations"

| Problem | Cause | Solution |
|---------|-------|----------|
| Module or its type definitions not found | Missing `@types/x` package | Install `@types/x` or add a `declare module 'x'` declaration |

## C#

### "NullReferenceException: Object reference not set to an instance of an object"

| Problem | Cause | Solution |
|---------|-------|----------|
| Accessing a null object | Variable is null when used | Enable nullable reference types. Use null checks: `if (obj != null)`. Use `?.` (null conditional) and `??` (null coalescing) |

### "CS1061: 'Type' does not contain a definition for 'Method'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Method doesn't exist on the type | Wrong type, missing using directive, or method is in a base class | Check the type. Add `using` directive if needed. Cast to the correct type |

### "CS0246: The type or namespace name 'X' could not be found"

| Problem | Cause | Solution |
|---------|-------|----------|
| Type not found | Missing `using` or missing NuGet package | Add `using X;` or install the NuGet package: `dotnet add package X` |

### "CS5001: Program does not contain a static 'Main' method suitable for an entry point"

| Problem | Cause | Solution |
|---------|-------|----------|
| No entry point found | Missing `Main` method or wrong signature | Ensure `Program.Main` exists. For top-level statements, ensure the file is configured correctly |

## C++

### "Segmentation fault (core dumped)"

| Problem | Cause | Solution |
|---------|-------|----------|
| Invalid memory access | Null pointer dereference, buffer overflow, use-after-free | Use smart pointers instead of raw pointers. Enable AddressSanitizer (`-fsanitize=address`) |

### "undefined reference to 'X'"

| Problem | Cause | Solution |
|---------|-------|----------|
| Linker error | Function declared but not defined, or library not linked | Check that the definition exists and is compiled. Link the correct library: `-lX` |

### "expected ';' at end of member declaration"

| Problem | Cause | Solution |
|---------|-------|----------|
| Syntax error | Missing semicolon after class definition | Add `;` after the closing brace of a class or struct |

### "error: 'X' was not declared in this scope"

| Problem | Cause | Solution |
|---------|-------|----------|
| Name not found | Variable or function not declared, or wrong namespace | Check spelling, include the correct header, use the correct namespace qualifier |

## SQL

### "no such table: X" (SQLite) / "relation 'X' does not exist" (PostgreSQL)

| Problem | Cause | Solution |
|---------|-------|----------|
| Table not found | Table doesn't exist or wrong database | Check `SELECT name FROM sqlite_master;` or `SELECT table_name FROM information_schema.tables;` |

### "UNIQUE constraint failed"

| Problem | Cause | Solution |
|---------|-------|----------|
| Duplicate value | Inserting a value that violates a unique constraint | Check the existing values. Use `INSERT OR IGNORE` or `ON CONFLICT DO UPDATE` |

### "FOREIGN KEY constraint failed"

| Problem | Cause | Solution |
|---------|-------|----------|
| Referenced row doesn't exist | Inserting a foreign key value that has no matching row | Insert the parent row first, or check the value being inserted |

### "syntax error at or near 'X'"

| Problem | Cause | Solution |
|---------|-------|----------|
| SQL syntax error | Wrong keyword, missing comma, wrong order | Check the query structure. Use parameterized queries to avoid string concatenation issues |

## General Diagnostics

| Problem | Approach |
|---------|----------|
| Error message is cryptic | Search the exact error message. It's almost certainly been asked before |
| Code compiles but does nothing | Add logging or print statements. Use a debugger to trace execution |
| Different results on different machines | Check versions (language, runtime, libraries). Check environment variables and OS differences |
| "Works on my machine" | Check OS, runtime version, installed packages. Use containers for reproducible environments |
