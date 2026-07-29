# What Is Testing?

> Verifying that software behaves correctly — systematically, repeatably, and automatically.

> **Related:** [Unit Testing](unit-testing.md) | [Integration Testing](integration-testing.md) | [End-to-End Testing](end-to-end-testing.md)

---

## What Is It?

Software testing is the practice of running code against expected outcomes to catch bugs, prevent regressions, and document intended behavior. Automated tests are scripts that do this without human intervention.

## The Test Pyramid

```
        /\  E2E  /\           Few, slow, broad confidence
       /  --------\
      / Integration \         Some, medium speed
     /----------------\
    /     Unit Tests     \     Many, fast, precise
   /----------------------\
```

| Level | Speed | Count | What It Catches | Tools |
|-------|-------|-------|-----------------|-------|
| Unit | Fast | Many | Logic bugs in a single function | pytest, Jest |
| Integration | Medium | Some | Interface mismatches, data flow | pytest + HTTP, supertest |
| E2E | Slow | Few | User-facing regressions, workflow breaks | Playwright, Cypress |

## When to Test What

| Type | What | Example |
|------|------|---------|
| Unit | A single function or method | `calculate_total(quantity, price)` |
| Integration | Two or more components | API endpoint → database query |
| E2E | A user journey | Login → search → checkout |
| Smoke | Critical path sanity | App boots, homepage loads |
| Regression | Previously fixed bugs | Old bug doesn't come back |
| Acceptance | Meets requirements | Stakeholder signs off |

## Test Naming Conventions

| Style | Example |
|-------|---------|
| Given-when-then | `given_user_is_logged_in_when_they_view_profile_then_shows_email` |
| Unit-describe | `test_add_returns_sum_of_two_numbers` |
| BDD-style | `should_redirect_to_login_when_not_authenticated` |

## Best Practices

- **Test behavior, not implementation** — tests should pass after refactoring
- **One assertion concept per test** — not necessarily one assertion, but one logical check
- **Isolate tests** — no shared state between tests
- **Fast feedback** — unit tests should run in milliseconds
- **Deterministic** — same test, same result, every time
- **Independent** — tests can run in any order, in parallel

## What's Next?

Start with [Unit Testing](unit-testing.md) for the fundamentals, then move to [Integration](integration-testing.md) and [E2E](end-to-end-testing.md) as your project grows.
