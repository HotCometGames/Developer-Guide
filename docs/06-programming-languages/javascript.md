# JavaScript

> The language of the web — dynamic, event-driven, and running everywhere from browsers to servers.

> **Related:** [TypeScript](typescript.md) | [HTML & CSS](html-and-css.md)

---

## What Is It?

JavaScript is a dynamically-typed, interpreted language that runs in every web browser. With Node.js, it also runs on servers, desktops (Electron), and even robots. It's the only language natively supported by browsers, making it the universal language of web frontend.

## When to Use JavaScript

| Use Case | Good Fit? |
|----------|-----------|
| Web frontend | Required (the only browser language) |
| Web backend (Node.js) | Excellent |
| Desktop apps (Electron, Tauri) | Good |
| Mobile apps (React Native) | Good |
| Game development (web) | Good |
| Scripting | Good |
| Systems programming | Poor |

## Key Features

### Dynamic & Loosely Typed

```javascript
let x = 5;        // number
x = "hello";      // string — no error
```

This flexibility is powerful but error-prone. TypeScript adds static types on top of JavaScript.

### Event Loop & Async

JavaScript runs on a single thread with an event loop. Asynchronous operations don't block:

```javascript
// Promises
fetch("/api/data")
  .then(response => response.json())
  .then(data => console.log(data));

// Async/await (syntactic sugar over Promises)
async function loadData() {
  const response = await fetch("/api/data");
  const data = await response.json();
  return data;
}
```

### Prototypal Inheritance

Unlike classical OOP languages, JavaScript uses prototypal inheritance — objects inherit from other objects.

### First-Class Functions

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);
```

## Ecosystem

| Category | Tools |
|----------|-------|
| Runtime | Node.js, Deno, Bun |
| Frontend frameworks | React, Vue, Svelte, Solid |
| Backend frameworks | Express, Fastify, Next.js |
| Testing | Vitest, Jest, Playwright |
| Linting | ESLint |
| Formatting | Prettier |
| Package management | npm, yarn, pnpm, bun |
| Bundling | Vite, esbuild, webpack |
| Type checking | TypeScript |

## Modules (ESM)

```javascript
// math.js
export function add(a, b) { return a + b; }

// app.js
import { add } from "./math.js";
```

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| `==` vs `===` | `==` coerces types (`5 == "5"` is `true`) | Always use `===` |
| `this` binding | `this` depends on call context, not definition | Use arrow functions or `.bind()` |
| Floating point | `0.1 + 0.2 !== 0.3` | Round to fixed decimal places |
| Async error handling | Unhandled promise rejections crash Node | Always use `.catch()` or `try/catch` with `await` |
| `var` vs `let`/`const` | `var` has function scope, not block scope | Prefer `const`, use `let` when reassigning |

## Best Practices

- **Use `const` by default, `let` when you must reassign** — never use `var`
- **Always use `===`** — avoid type coercion surprises
- **Use async/await** — cleaner than raw `.then()` chains
- **Format with Prettier** — consistent code style across the team
- **Lint with ESLint** — catch common errors before they ship
- **Prefer modern ES modules** over CommonJS (`require`)
- **Write tests** — Vitest or Jest for unit tests, Playwright for browser tests
