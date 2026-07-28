# Learning a New Language

> A systematic approach to picking up any programming language — faster, with deeper understanding.

> **Related:** [What Is a Programming Language?](what-is-a-programming-language.md) | [Choosing a Language](choosing-a-language.md)

---

## What Is It?

Once you know one language well, learning another is about mapping concepts, not starting from zero. This page gives you a framework to learn any language efficiently.

## The Universal Checklist

Every language has these features. Find them first:

| Concept | Questions to Answer |
|---------|-------------------|
| Variables | How do you declare? Mutable vs immutable? Type inference? |
| Functions | How do you define and call? Default args? Variadic? Named params? |
| Control flow | `if`, `else`, `switch`, `match`, loops (`for`, `while`) |
| Data structures | Arrays, lists, maps, sets, tuples, structs |
| Error handling | Exceptions? Result types? Error codes? Panics? |
| Types | Static/dynamic? Strong/weak? Nullable? Generics? |
| Memory model | Stack vs heap? GC? Ownership? Manual? |
| Modules | Files, packages, imports, exports |
| Testing | Built-in test framework? Assertions? |
| Toolchain | Compiler/interpreter, package manager, build system, formatter |

## Learning Strategy

### Phase 1: Syntax (Day 1)

Write "Hello, World" and the FizzBuzz program. This forces you to learn:

- File structure and entry point
- Print/console output
- Variables and basic types
- Conditionals and loops
- Functions

### Phase 2: Patterns (Days 2-5)

Implement familiar algorithms in the new language:

```python
# Python — easy to read
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b
```

```rust
// Rust — same algorithm, different syntax
fn fibonacci(n: u32) -> impl Iterator<Item = u32> {
    let mut a = 0;
    let mut b = 1;
    (0..n).map(move |_| {
        let result = a;
        a = b;
        b = result + b;
        result
    })
}
```

### Phase 3: Idioms (Days 5-14)

Learn how the language *wants* to be used — not just what's possible, but what's idiomatic:

- Read the language's official style guide
- Look at well-known open-source projects
- Identify patterns that are unique to the language
- Learn the standard library

### Phase 4: Deep (Weeks 3-8)

- Memory model and performance characteristics
- Concurrency primitives
- Metaprogramming / macros
- FFI / interop with other languages
- Advanced type system features

## Resources by Language

| Language | Official Docs | Practice |
|----------|-------------|----------|
| Python | [docs.python.org](https://docs.python.org/3/) | Exercism Python track |
| TypeScript | [typescriptlang.org](https://www.typescriptlang.org/docs/) | TypeScript playground |
| C# | [learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/csharp/) | Exercism C# track |
| C++ | [cppreference.com](https://en.cppreference.com/) | Exercism C++ track |
| Rust | [doc.rust-lang.org](https://doc.rust-lang.org/book/) | Rustlings exercises |
| Go | [go.dev/doc](https://go.dev/doc/) | Tour of Go |
| SQL | Various by dialect | SQLBolt, PGExercises |

## Common Transfer Pitfalls

| Mistake | Example | Fix |
|---------|---------|-----|
| Writing Python in C# | Using dynamic typing everywhere | Learn C#'s type system and idioms |
| Writing C# in Python | Overusing classes for everything | Use modules, functions, and comprehensions |
| Writing JavaScript in TypeScript | Overusing `any` | Enable `strict` mode and learn the type system |
| Writing C++ in Rust | Using raw pointers everywhere | Embrace the borrow checker — it's not fighting you, it's helping |
| Ignoring the ecosystem | Reimplementing standard library features | Check what's built-in before writing custom code |

## Best Practices

- **Build something real** — tutorial projects don't stick. Build something you need
- **Read other people's code** — you learn idioms by reading, not writing
- **Use AI as a learning tool** — ask "what's the idiomatic way to do X in [language]?"
- **Learn one language at a time** — context-switching between new languages slows learning
- **Understand the "why"** — language features exist for a reason. Understanding the motivation makes them easier to remember
- **Write lots of bad code** — you can't write good code until you've written enough bad code to know the difference
