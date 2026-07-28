# Choosing a Language

> How to pick the right programming language for your project.

> **Related:** [What Is a Programming Language?](what-is-a-programming-language.md) | [Learning a New Language](learning-new-languages.md)

---

## What Is It?

There's no single "best" language. The right choice depends on your problem domain, team, performance needs, and ecosystem. This page helps you evaluate trade-offs systematically.

## Decision Factors

### 1. Domain

| Domain | Strong Contenders |
|--------|-------------------|
| Web frontend | JavaScript, TypeScript |
| Web backend | Python, TypeScript, C#, Go, Rust |
| Game development | C# (Unity), C++ (Unreal), GDScript (Godot) |
| Mobile apps | C# (Xamarin/Maui), JavaScript (React Native) |
| Data science / ML | Python, R |
| Systems programming | Rust, C, C++, Go |
| Desktop apps | C# (.NET), JavaScript (Electron), Rust (Tauri) |
| Scripting / automation | Python, PowerShell, Bash |
| Databases | SQL (any dialect) |

### 2. Performance Requirements

| Need | Consider |
|------|----------|
| Maximum performance | C, C++, Rust, Zig |
| Good performance with safety | Rust, Go, C# |
| Good enough performance | Python, JavaScript, TypeScript |
| Throughput at scale | Go, Rust, C#, Java |
| Latency-sensitive | C, C++, Rust |

### 3. Team & Ecosystem

- **Available talent** — can you hire or train for this language?
- **Library maturity** — does the language have well-maintained libraries for your domain?
- **Tooling** — editors, debuggers, profilers, package managers
- **Community** — Stack Overflow, forums, Discord servers, conferences
- **Longevity** — is the language growing or declining?

### 4. Development Speed

| Language | Prototyping Speed | Maintenance Cost | Notes |
|----------|------------------|------------------|-------|
| Python | Fastest | Medium | Dynamic typing catches up in large codebases |
| TypeScript | Fast | Low | Type safety reduces maintenance burden |
| C# | Fast | Low | Great tooling, static typing |
| Go | Fast | Low | Simple, opinionated, easy to read |
| C++ | Slow | High | Full control but high cognitive load |
| Rust | Medium | Low | Compiler catches everything, steep learning curve |

### 5. Ecosystem & Tooling

| Factor | What to Check |
|--------|--------------|
| Package manager | npm, pip, cargo, NuGet, go modules |
| Build system | webpack, esbuild, MSBuild, CMake, cargo |
| Testing frameworks | pytest, Jest, NUnit, go test |
| Deployment | Docker support, serverless support, cloud SDKs |
| CI/CD | GitHub Actions templates, cloud build pipelines |

## Language Comparison Table

| Language | Typing | Memory | Compile/Runtime | GC | Best For |
|----------|--------|--------|-----------------|----|----------|
| Python | Dynamic | Managed | Interpreted | Yes | Scripting, data science, backend |
| JavaScript | Dynamic | Managed | Interpreted | Yes | Web frontend, backend (Node) |
| TypeScript | Static | Managed | Compiled to JS | Yes | Large-scale web apps |
| C# | Static | Managed | JIT-compiled | Yes | Games, desktop, backend |
| C++ | Static | Manual | Compiled | No | Systems, games, performance |
| SQL | N/A | N/A | Interpreted | N/A | Data querying |
| Rust | Static | Ownership | Compiled | No | Systems, performance-critical |

## Decision Flow

1. **What am I building?** → narrow to 2-3 candidates by domain
2. **Who is building it?** → eliminate languages your team doesn't know (or factor in learning time)
3. **How fast does it need to be?** → eliminate languages that can't meet performance
4. **What ecosystem exists?** → verify libraries and tooling support your use case
5. **Pick the simplest option** — unless you need the complexity

## What's Next?

Dive into a specific language: [Python](python.md), [JavaScript](javascript.md), [TypeScript](typescript.md), [C#](csharp.md), [C++](cpp.md), [SQL](sql.md), or [HTML & CSS](html-and-css.md).
