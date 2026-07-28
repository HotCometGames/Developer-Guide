# Python

> A dynamically-typed, interpreted language known for readability, versatility, and a vast ecosystem.

> **Related:** [Choosing a Language](choosing-a-language.md) | [TypeScript](typescript.md)

---

## What Is It?

Python is a high-level, dynamically-typed programming language designed for readability. It's used across web development, data science, automation, scripting, and increasingly in game development (Pygame, Godot GDScript-like syntax).

## When to Use Python

| Use Case | Good Fit? |
|----------|-----------|
| Scripting & automation | Excellent |
| Data science & ML | Industry standard |
| Web backend (Django, FastAPI) | Excellent |
| Game prototyping | Good (Pygame, Arcade) |
| Desktop apps | OK (Tkinter, PyQt) |
| Mobile apps | Poor (rarely used) |
| Systems programming | Poor (performance overhead) |

## Key Features

### Dynamic Typing

```python
x = 5           # int
x = "hello"     # str — no error, same variable
```

### Type Hints (Optional)

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

Use `mypy` to check types statically — type hints are ignored at runtime.

### First-Class Functions

```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
evens = [x for x in numbers if x % 2 == 0]
```

### Context Managers

```python
with open("file.txt", "r") as f:
    content = f.read()
# File is automatically closed
```

## Ecosystem

| Category | Tools |
|----------|-------|
| Web frameworks | Django, FastAPI, Flask |
| Data science | NumPy, pandas, scikit-learn, PyTorch, Jupyter |
| Testing | pytest, unittest, coverage |
| Linting | ruff, pylint, mypy |
| Formatting | black, ruff format |
| Package management | pip, uv, poetry, conda |
| ORM | SQLAlchemy, Django ORM |

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| Mutable default args | `def f(lst=[]):` — the list is shared across calls | Use `None` and create inside: `def f(lst=None):` |
| Late binding closures | `[lambda: i for i in range(5)]` all return 4 | Use default arg: `lambda i=i: i` |
| Global interpreter lock (GIL) | Only one thread executes Python bytecode | Use `multiprocessing` or async IO for concurrency |
| Silent type errors | `"2" + 2` raises TypeError | Use type hints + mypy |

## Best Practices

- **Follow PEP 8** — use `ruff` or `black` for formatting
- **Use virtual environments** — `uv venv` or `python -m venv .venv`
- **Write type hints** — they catch bugs and document code
- **Prefer comprehensions** over `map`/`filter` with lambdas
- **Use pathlib** instead of `os.path` — `Path("dir") / "file.txt"`
- **Write pytest tests** — `assert`-based, no boilerplate
