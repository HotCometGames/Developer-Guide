# Testing Troubleshooting

> Common testing failures and how to fix them.

---

## Flaky Tests

| Problem | Cause | Fix |
|---------|-------|-----|
| Test passes locally, fails in CI | Environment differences | Match CI environment (OS, timezone, locale) |
| Test fails intermittently | Race condition | Add proper awaits, use `waitFor`/`expect.poll` |
| Test depends on test order | Shared mutable state | Reset state in `beforeEach`/fixture setup |
| Test fails only on Monday | Date-dependent logic | Mock dates in tests |
| Network-dependent test | External API down | Mock external calls, test integration separately |

## Slow Test Suite

| Cause | Fix |
|-------|-----|
| Too many E2E tests | Move coverage down the test pyramid |
| Database setup per test | Use shared fixtures with `session` scope |
| No parallel execution | `pytest -n auto` or `vitest --pool=threads` |
| Expensive mocks | Reduce mock depth, use lightweight fakes |
| Large snapshot files | Review and reduce snapshot sizes |

## CI Failures

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Tests pass locally but fail on CI | Missing env vars | Set `CI=true` compatible defaults |
| Timeout in CI only | Slower CI runner | Increase test timeouts for CI |
| Screenshot mismatch | Different screen size/resolution | Use consistent viewport in config |
| Test order-dependent | Shared file/database state | Isolate per-test data |

## Common Errors

| Error | Meaning | Fix |
|-------|---------|-----|
| `ModuleNotFoundError` | Import broken | Check `PYTHONPATH` / `NODE_PATH` |
| `No tests found` | Wrong file pattern | Check test discovery config |
| `Segmentation fault` | Native extension crash | Run with `-v` to find which test triggers it |
| `Out of memory` | Test leaks memory | Check for unclosed connections/file handles |
| `Port already in use` | Previous server didn't stop | Kill orphan processes between test runs |

## Debugging Failing Tests

```bash
# pytest — show locals on failure
pytest -l

# pytest — drop into debugger on failure
pytest --pdb

# Jest/Vitest — run with inspect
npx vitest --inspect-brk

# Playwright — open trace viewer on failure
npx playwright show-report
```

## Best Practices for Reliable Tests

- **Run tests in order-independent mode** — CI runs them in random order by default
- **Set CI to fail-fast** — `pytest -x` to stop on first failure
- **Log CI traces** — screenshots, videos, and logs for every failing E2E test
- **Quarantine flaky tests** — move unreliable tests to a separate suite, don't ignore them

---

> **Related:** [Unit Testing](unit-testing.md) — test fundamentals | [CI/CD Pipelines](../13-deployment/ci-cd-pipelines.md) — running tests in CI
