# JavaScript Testing

> Jest and Vitest patterns for testing JavaScript and TypeScript projects.

> **Related:** [Python Testing](python-testing.md) | [Unit Testing](unit-testing.md) | [End-to-End Testing](end-to-end-testing.md)

---

## What Is It?

The JavaScript ecosystem has two dominant test runners: **Jest** (mature, batteries-included) and **Vitest** (fast, Vite-native, Jest-compatible API).

## Setup

```bash
# Jest
npm install --save-dev jest
npx jest --init

# Vitest
npm install --save-dev vitest
```

```javascript
// vitest.config.ts (or jest.config.js)
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
    coverage: {
      provider: 'v8',
      reporter: ['text', 'html'],
      thresholds: {
        lines: 80,
        branches: 70,
        functions: 80,
      },
    },
  },
});
```

## Basic Tests

```javascript
// sum.js
export function sum(a, b) {
  return a + b;
}

// sum.test.js
import { expect, test } from 'vitest';
import { sum } from './sum';

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

## Matchers

| Matcher | Asserts | Example |
|---------|---------|---------|
| `toBe` | Reference equality | `expect(x).toBe(3)` |
| `toEqual` | Deep equality | `expect(obj).toEqual({ a: 1 })` |
| `toStrictEqual` | Deep + type + extra props | `expect(obj).toStrictEqual({ a: 1 })` |
| `toBeNull` | null | `expect(x).toBeNull()` |
| `toBeDefined` | Not undefined | `expect(x).toBeDefined()` |
| `toContain` | Array/string includes | `expect([1,2]).toContain(1)` |
| `toThrow` | Throws error | `expect(fn).toThrow()` |
| `toHaveLength` | `.length` | `expect(arr).toHaveLength(3)` |
| `toMatchObject` | Object subset | `expect(obj).toMatchObject({ a: 1 })` |

## Mocks

```javascript
// Mock a module
vi.mock('./email');
import { sendEmail } from './email';

test('sends welcome email', () => {
  sendEmail.mockResolvedValue({ status: 'sent' });
  const result = await welcomeUser('alice@example.com');
  expect(sendEmail).toHaveBeenCalledWith('alice@example.com', 'Welcome!');
  expect(sendEmail).toHaveBeenCalledTimes(1);
});

// Mock a function
const mockFn = vi.fn();
mockFn.mockReturnValue(42);
mockFn.mockResolvedValue({ data: 'async result' });
mockFn.mockImplementation((x) => x * 2);
```

## Testing Components with Testing Library

```javascript
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments counter', () => {
  render(<Counter />);
  fireEvent.click(screen.getByRole('button', { name: /increment/i }));
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

### Testing Library Principles

- Tests interact with components the way users do — by finding elements by role, label, or text
- Avoid testing internal state or implementation details
- Prefer `getByRole`, `getByLabelText`, `getByText` over CSS selectors

## Snapshot Testing

```javascript
test('component renders correctly', () => {
  const { container } = render(<MyComponent />);
  expect(container).toMatchSnapshot();
});
```

| Question | Answer |
|----------|--------|
| Good for | Catching unexpected UI changes |
| Bad for | Large snapshots (review burden), frequently changing UI |
| Update | `npx jest -u` or `npx vitest -u` |

## Run Commands

| Task | Jest | Vitest |
|------|------|--------|
| Run all | `npx jest` | `npx vitest run` |
| Watch mode | `npx jest --watch` | `npx vitest` (default) |
| Coverage | `npx jest --coverage` | `npx vitest run --coverage` |
| Specific file | `npx jest path/file.test.js` | `npx vitest run path/file.test.js` |
| UI mode | — | `npx vitest --ui` |

## Best Practices

- **Use `describe` blocks** to group related tests with shared setup
- **Reset mocks between tests** — `afterEach(() => { vi.clearAllMocks(); })`
- **Prefer `toEqual` over `toBe`** for objects and arrays
- **Test through the public API** — for React, this means Testing Library queries
- **Don't snapshot large trees** — they become noise in code review

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Testing implementation details | Brittle tests | Use Testing Library queries |
| Over-mocking | Tests pass, production breaks | Mock only at module boundaries |
| Snapshot everything | Unreviewable changes | Use targeted assertions, not snapshots |
| No `cleanup` | State leaks between tests | Vitest/Jest handle this for React |

## What's Next?

Apply these patterns with [Unit Testing](unit-testing.md) concepts, or move to [End-to-End Testing](end-to-end-testing.md) with Playwright for full browser tests.
