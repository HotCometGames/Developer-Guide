# What Is a Programming Language?

> A formal language for instructing a computer — the bridge between human intent and machine execution.

> **Related:** [Choosing a Language](choosing-a-language.md) | [Learning a New Language](learning-new-languages.md)

---

## What Is It?

A programming language is a set of rules for writing instructions that a computer can execute. It provides syntax (form) and semantics (meaning) to express algorithms, manipulate data, and control hardware.

## Compiled vs Interpreted

| Aspect | Compiled | Interpreted |
|--------|----------|-------------|
| How it runs | Source → machine code → execute | Source → execute on the fly |
| Speed | Faster (pre-translated) | Slower (translated at runtime) |
| Development cycle | Edit → compile → run | Edit → run (no compile step) |
| Portability | Platform-specific binary | Any platform with a runtime |
| Examples | C, C++, Rust, Go | Python, JavaScript, Ruby |

Some languages blur the line. C# compiles to IL (intermediate language) and JIT-compiles at runtime. TypeScript compiles to JavaScript.

## Static vs Dynamic Typing

| Aspect | Static Typing | Dynamic Typing |
|--------|--------------|----------------|
| When types are checked | At compile time | At runtime |
| Speed | Faster (optimized at compile time) | Slower (type checking at runtime) |
| Safety | Catches type errors before running | Type errors appear at runtime |
| Flexibility | Less flexible, more structured | More flexible, less structured |
| Examples | TypeScript, C#, C++, Rust | Python, JavaScript, Ruby |

### Gradual Typing

Some languages support gradual typing — start dynamic, add types as you go:

- **TypeScript** — all JavaScript + optional types
- **Python** — type hints via `mypy` (not enforced at runtime)
- **C#** — `var` for inferred types, `dynamic` for dynamic behavior

## Programming Paradigms

| Paradigm | What It Emphasizes | Languages |
|----------|-------------------|-----------|
| **Imperative** | Step-by-step instructions | C, Python, JavaScript |
| **Object-Oriented** | Objects with data + behavior | C#, Java, Python, TypeScript |
| **Functional** | Pure functions, immutability | Haskell, F#, Elixir, Rust |
| **Procedural** | Functions and procedures | C, Pascal, Go |
| **Declarative** | What to do, not how | SQL, HTML, CSS |

Most modern languages are **multi-paradigm** — you can use OOP, functional, and imperative styles in the same language.

## Memory Management

| Strategy | How It Works | Languages |
|----------|-------------|-----------|
| **Manual** | You allocate and free memory | C, C++ |
| **Garbage Collection** | Runtime automatically reclaims unused memory | C#, Java, Python, JavaScript, Go |
| **Ownership** | Compiler tracks ownership and lifetimes at compile time | Rust |

## Language Levels

| Level | Abstraction | Examples |
|-------|-----------|----------|
| Low-level | Close to hardware, manual control | Assembly, C |
| Mid-level | Some abstraction, memory control | C++, Rust |
| High-level | Abstracted from hardware, memory-safe | Python, JavaScript, C#, Go |
| Very high-level | Domain-specific, minimal boilerplate | SQL, HTML, CSS |

## What's Next?

If you're choosing a language for a project, see [Choosing a Language](choosing-a-language.md). For hands-on syntax, see the language-specific pages.
