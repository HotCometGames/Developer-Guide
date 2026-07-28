# TypeScript

> JavaScript with static types — catching errors at compile time while keeping the JS ecosystem.

> **Related:** [JavaScript](javascript.md) | [Choosing a Language](choosing-a-language.md)

---

## What Is It?

TypeScript is a superset of JavaScript that adds optional static typing. It compiles to plain JavaScript, runs anywhere JS runs, and adds no runtime overhead — all type checks happen at compile time.

## Why TypeScript?

| Aspect | JavaScript | TypeScript |
|--------|------------|------------|
| Type checking | Runtime only | Compile time |
| Error discovery | When code runs | When code is written |
| Autocomplete | Limited by editor inference | Rich, from type definitions |
| Refactoring | Manual, risky | Tool-assisted, safe |
| Self-documenting | No type information | Types serve as documentation |
| Learning curve | Low | Medium |

## Key Features

### Type Annotations

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

const age: number = 30;
const isActive: boolean = true;
```

### Interfaces & Types

```typescript
interface User {
  id: number;
  name: string;
  email?: string;       // optional property
  readonly createdAt: Date;  // immutable after creation
}

type Status = "active" | "inactive" | "banned";

function updateUser(user: User, status: Status): User {
  return { ...user };
}
```

### Generics

```typescript
function firstElement<T>(arr: T[]): T | undefined {
  return arr[0];
}

const first = firstElement([1, 2, 3]);  // type: number
```

### Union & Intersection Types

```typescript
type StringOrNumber = string | number;
type Admin = User & { role: "admin" };
```

### Type Narrowing

```typescript
function process(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}
```

## TypeScript Configuration

```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2022",
    "module": "ESNext",
    "outDir": "./dist",
    "rootDir": "./src",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

| Option | What It Does |
|--------|-------------|
| `strict: true` | Enables all strict checks (recommended) |
| `target` | JS output version |
| `module` | Module system for output |
| `noUncheckedIndexedAccess` | Prevents accessing arrays without bounds check |
| `exactOptionalPropertyTypes` | Stricter optional property handling |

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| `any` type | Opts out of type checking entirely, defeats TS's purpose | Use `unknown` instead, then narrow |
| Non-null assertions (`!`) | `obj!.prop` — suppresses null checks | Use proper null handling with `if` checks |
| Loose `tsconfig.json` | Without `strict: true`, many types aren't checked | Enable `strict: true` |
| Overly complex types | Type gymnastics that are hard to read | Prefer simple types. Extract complex ones into type aliases |
| Not using `satisfies` | `const x = {a: 1} satisfies Record<string, number>` type-checks without widening | New in TS 4.9 |

## Migration from JavaScript

1. Add `tsconfig.json` with `allowJs: true` and `checkJs: true`
2. Rename `.js` files to `.ts` gradually
3. Add types file by file, starting with the most-used modules
4. Enable `strict` once the codebase is mostly typed
5. Use `@ts-expect-error` as a temporary escape hatch

## Best Practices

- **Enable `strict: true`** — without it, TypeScript catches very few bugs
- **Prefer `interface` for object shapes** — they extend and merge; `type` for unions and primitives
- **Use `unknown` instead of `any`** — forces type checking before use
- **Leverage `readonly`** — immutable properties catch mutation bugs
- **Use discriminated unions** for state management — one field determines the variant
- **Run `tsc --noEmit` in CI** — type-check without emitting JavaScript
