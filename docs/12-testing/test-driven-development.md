# Test-Driven Development

> Writing the test before the code — red, green, refactor.

> **Related:** [Unit Testing](unit-testing.md) | [What Is Testing?](what-is-testing.md)

---

## What Is It?

TDD is a development practice where you write a failing test (red), write the minimal code to make it pass (green), then improve the code without changing its behavior (refactor).

```
Red    →  Write a test that fails
  ↓
Green  →  Write the simplest code to pass
  ↓
Refactor →  Clean up without changing behavior
  ↓
(Repeat)
```

## The Cycle

### 1. Red — Write a Failing Test

```python
# Before writing any implementation
def test_calculate_total():
    assert calculate_total(3, 10.0) == 30.0  # doesn't exist yet → fails
```

### 2. Green — Make It Pass

```python
def calculate_total(quantity, price):
    return quantity * price  # simplest thing that works
```

### 3. Refactor — Improve the Code

```python
def calculate_total(quantity: int, price: float) -> float:
    """Calculate total price before tax."""
    return quantity * price
```

## When TDD Helps

| Scenario | Why TDD Works |
|----------|---------------|
| Complex business logic | Tests clarify what "correct" means |
| Bug fixes | Write a test that reproduces the bug, then fix |
| Refactoring legacy code | Test the behavior first, then safely restructure |
| API or library design | Tests become the first consumer of your design |
| Collaboration | Tests document expected behavior for the team |

## When to Skip TDD

| Scenario | Alternative |
|----------|-------------|
| Rapid prototyping | Spike first, then TDD the production version |
| UI exploration | Use manual testing or visual tools, then E2E test |
| One-off scripts | Smoke test manually |
| You don't know what "correct" looks like | Explore first, then write tests |

## Best Practices

- **Write the simplest test that expresses the requirement** — don't test the framework
- **Write the simplest code that passes** — no premature abstraction
- **Keep the cycle tight** — seconds per loop, not minutes
- **If the test is hard to write** — the design may need improvement
- **Refactor with confidence** — the passing test proves you didn't break anything

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Writing too-large tests | Slow cycle, hard to pin failures | Test one behavior at a time |
| Skipping refactor step | Code quality degrades | Always clean up in green |
| Testing via the UI in TDD | Brittle, slow tests | Use unit TDD, not E2E TDD |
| Golden hammer | TDD isn't always the answer | Use judgment: TDD for logic, not exploration |

## What's Next?

TDD works best with well-structured [Unit Tests](unit-testing.md). For a broader view of the testing landscape, revisit [What Is Testing?](what-is-testing.md).
