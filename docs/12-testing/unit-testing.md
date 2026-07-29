# Unit Testing

> Testing individual functions, methods, or classes in isolation from their dependencies.

> **Related:** [Python Testing](python-testing.md) | [JavaScript Testing](javascript-testing.md) | [Test-Driven Development](test-driven-development.md)

---

## What Is It?

A unit test exercises a single unit of code — typically one function or method — with controlled inputs and asserts the outputs. External dependencies (databases, APIs, file systems) are replaced with test doubles.

## Test Doubles

| Type | What It Does | Example |
|------|-------------|---------|
| Stub | Returns a fixed value | A function that always returns `42` |
| Mock | Records how it was called | Assert that `send_email` was called with the right args |
| Fake | A lightweight working implementation | An in-memory database instead of Postgres |
| Spy | Wraps a real object to record calls | Track how many times `logger.info` was called |
| Dummy | Passed around but never used | An empty object to satisfy a constructor |

```
Real object:  database.save(user)   → writes to Postgres
Stub:         database.save(user)   → returns true
Mock:         database.save(user)   → records call, returns true
Fake:         database.save(user)   → appends to in-memory list
```

## Coverage

Coverage measures which lines of code are executed during tests. It's a floor, not a target.

| Metric | What It Measures | Typical Target |
|--------|-----------------|----------------|
| Line coverage | Lines executed | 80%+ |
| Branch coverage | If/else paths taken | 70%+ |
| Function coverage | Functions called | 90%+ |

```bash
# pytest with coverage
pytest --cov=src --cov-report=term-missing

# Jest with coverage
npx jest --coverage
```

> **Warning:** 100% coverage does not mean bug-free code. Tests can assert nothing useful while covering every line.

## Parametrization

One test, many input/output pairs:

```python
# pytest
@pytest.mark.parametrize("input,expected", [
    (1, 2), (2, 4), (3, 6),
])
def test_double(input, expected):
    assert input * 2 == expected
```

```javascript
// Jest
test.each([[1, 2], [2, 4], [3, 6]])(
  'double(%i) === %i',
  (input, expected) => {
    expect(input * 2).toBe(expected);
  }
);
```

## FIRST Principles

| Letter | Principle | Why |
|--------|-----------|-----|
| F | Fast | Slow tests don't get run |
| I | Isolated | Tests don't depend on each other |
| R | Repeatable | Same result every time, anywhere |
| S | Self-validating | Pass/fail, no manual inspection |
| T | Timely | Written with or before the code |

## Best Practices

- **Arrange-Act-Assert** — structure each test in three clear phases
- **Test the public API** — not private methods
- **One logical assertion per test** — if it fails, you know exactly what broke
- **Avoid logic in tests** — no `if`, `for`, or `try` in test code
- **Don't mock what you don't own** — wrap third-party APIs in your own abstraction

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Testing implementation details | Tests break on refactor | Test observable behavior |
| Over-mocking | Tests pass, production breaks | Mock only external boundaries |
| Shared mutable state | Tests fail in different order | Reset state in `beforeEach`/setup |
| Hard-coded values | Brittle tests | Use factories or builders |
| Skipping edge cases | Bugs at boundaries | Test empty, null, overflow, zero |

## What's Next?

Once you have solid unit tests, learn [Integration Testing](integration-testing.md) to verify your components work together.
