# Testing Quick Reference

> One-page reference for unit, integration, and e2e testing with pytest, Jest, and Playwright. Print this or bookmark it.

---

## pytest (Python)

### Basic

| Task | Command |
|------|---------|
| Run all | `pytest` |
| Run file | `pytest test_file.py` |
| Run test | `pytest test_file.py::test_name` |
| Verbose | `pytest -v` |
| Stop on fail | `pytest -x` |
| Show locals | `pytest -l` |
| Run last failed | `pytest --lf` |
| Run failed only | `pytest --ff` |
| With coverage | `pytest --cov=src` |
| Coverage report | `pytest --cov=src --cov-report=html` |

### Assertions

| Assertion | Example |
|-----------|---------|
| Equal | `assert result == expected` |
| Not equal | `assert result != expected` |
| True | `assert condition is True` |
| Raises | `pytest.raises(Exception, func)` |
| Approx | `assert result == pytest.approx(0.1)` |
| In | `assert item in collection` |
| Is None | `assert result is None` |
| Match regex | `assert re.match(r"pattern", s)` |

### Fixtures

```python
@pytest.fixture
def setup_data():
    data = {"key": "value"}
    yield data
    # teardown here

def test_something(setup_data):
    assert setup_data["key"] == "value"
```

### Parametrize

```python
@pytest.mark.parametrize("input,expected", [
    (1, 2),
    (2, 4),
    (3, 6),
])
def test_double(input, expected):
    assert input * 2 == expected
```

### Common Markers

| Marker | Purpose |
|--------|---------|
| `@pytest.mark.skip` | Skip test |
| `@pytest.mark.skipif(cond)` | Conditional skip |
| `@pytest.mark.xfail` | Expected failure |
| `@pytest.mark.parametrize` | Parameterize |
| `@pytest.mark.slow` | Custom marker |

## Jest (JavaScript/TypeScript)

### Basic

| Task | Command |
|------|---------|
| Run all | `npx jest` |
| Run file | `npx jest test_file.test.js` |
| Watch mode | `npx jest --watch` |
| Coverage | `npx jest --coverage` |
| Verbose | `npx jest --verbose` |
| Stop on fail | `npx jest --bail` |
| Update snapshots | `npx jest -u` |

### Assertions

| Assertion | Example |
|-----------|---------|
| Equal | `expect(result).toBe(expected)` |
| Deep equal | `expect(obj).toEqual(expected)` |
| True | `expect(cond).toBe(true)` |
| Null | `expect(val).toBeNull()` |
| Defined | `expect(val).toBeDefined()` |
| Close | `expect(val).toBeCloseTo(0.1)` |
| Throw | `expect(fn).toThrow(Error)` |
| Contain | `expect(str).toContain("sub")` |
| Length | `expect(arr).toHaveLength(3)` |
| Regex | `expect(str).toMatch(/regex/)` |

### Common Patterns

```javascript
// Setup/teardown
beforeEach(() => { /* before each test */ });
afterEach(() => { /* after each test */ });
beforeAll(() => { /* once before all */ });
afterAll(() => { /* once after all */ });

// Async
test('async test', async () => {
  const result = await fetchData();
  expect(result).toEqual({ data: 123 });
});

// Mock
jest.mock('./module');
const mockFn = jest.fn();
mockFn.mockReturnValue(42);
expect(mockFn).toHaveBeenCalled();
```

### Configuration (jest.config.js)

```javascript
module.exports = {
  testEnvironment: 'node',
  coverageDirectory: 'coverage',
  coverageThreshold: {
    global: { branches: 80, functions: 80, lines: 80 },
  },
};
```

## Playwright (E2E)

### Basic

| Task | Command |
|------|---------|
| Install | `npx playwright install` |
| Run all | `npx playwright test` |
| UI mode | `npx playwright test --ui` |
| Headed | `npx playwright test --headed` |
| Debug | `npx playwright test --debug` |
| Report | `npx playwright show-report` |
| Codegen | `npx playwright codegen url` |

### Common Test

```typescript
import { test, expect } from '@playwright/test';

test('homepage loads', async ({ page }) => {
  await page.goto('http://localhost:3000');
  await expect(page).toHaveTitle(/My App/);
  await expect(page.locator('h1')).toBeVisible();
});

test('form submission', async ({ page }) => {
  await page.goto('/form');
  await page.fill('#name', 'John');
  await page.click('button[type="submit"]');
  await expect(page.locator('.success')).toBeVisible();
});
```

### Selectors

| Selector | Example |
|----------|---------|
| CSS | `page.locator('.class')` |
| Text | `page.getByText('Submit')` |
| Role | `page.getByRole('button', { name: 'Submit' })` |
| Label | `page.getByLabel('Email')` |
| Placeholder | `page.getByPlaceholder('Enter email')` |
| Test ID | `page.getByTestId('submit-btn')` |

### Assertions

| Assertion | Example |
|-----------|---------|
| Visible | `await expect(locator).toBeVisible()` |
| Hidden | `await expect(locator).toBeHidden()` |
| Text | `await expect(locator).toHaveText('Hello')` |
| Value | `await expect(input).toHaveValue('text')` |
| URL | `await expect(page).toHaveURL('/done')` |
| Title | `await expect(page).toHaveTitle(/Home/)` |

## Test Pyramid

```
        /  E2E  \          Few, slow, high confidence
       /--------\
      /Integration\        Moderate count, moderate speed
     /--------------\
    /    Unit Tests    \    Many, fast, low-level
   /--------------------\
```

| Level | Speed | Count | Scope | Tools |
|-------|-------|-------|-------|-------|
| Unit | Fast | Many | Single function | pytest, Jest |
| Integration | Medium | Some | Multiple components | pytest, Jest |
| E2E | Slow | Few | Full user flow | Playwright, Cypress |

## TDD Cycle

```
Red → Green → Refactor
 │       │        │
 │       │        └── Improve code without changing behavior
 │       └── Write minimal code to pass
 └── Write a failing test first
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Testing implementation | Brittle tests | Test behavior, not internals |
| Mocking too much | False confidence | Mock external dependencies only |
| No test isolation | Flaky tests | Each test should be independent |
| Skipping cleanup | State leaks between tests | Use `afterEach`/fixtures |
| Testing everything | Slow suite | Follow test pyramid |
| No coverage target | Blind spots | Set minimum thresholds |

---

> **Full section:** [Testing](../12-testing/README.md) | **Next:** [Deployment](deployment-quick-reference.md)
