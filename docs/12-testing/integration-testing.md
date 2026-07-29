# Integration Testing

> Verifying that multiple components work together correctly.

> **Related:** [Unit Testing](unit-testing.md) | [End-to-End Testing](end-to-end-testing.md) | [Python Testing](python-testing.md)

---

## What Is It?

An integration test exercises two or more real components together — an API endpoint talking to a database, a service calling another service, or a message queue feeding a consumer. The goal is catching interface mismatches and data flow errors that unit tests miss.

## What to Integrate

| Pattern | What Connects | Example |
|---------|--------------|---------|
| Database | App code + database | Repository method with real SQLite |
| API | HTTP client + server | Request to FastAPI/Express endpoint |
| External service | App + third-party API | Payment gateway, email service |
| Message queue | Producer + consumer | Publishing to and reading from Redis |
| File system | App + disk | Reading/writing files |

## Test Databases

For integration tests that touch data:

```python
# pytest with SQLite in-memory
@pytest.fixture
def db():
    engine = create_engine("sqlite:///:memory:")
    Base.metadata.create_all(engine)
    yield engine
    Base.metadata.drop_all(engine)
```

```javascript
// Vitest with testcontainers
import { PostgreSqlContainer } from '@testcontainers/postgresql';

let container;
beforeAll(async () => {
  container = await new PostgreSqlContainer().start();
  process.env.DATABASE_URL = container.getConnectionUri();
}, 30_000);
```

| Approach | Speed | Isolation | Realism |
|----------|-------|-----------|---------|
| In-memory DB | Fast | Per test | Low — different dialect |
| Testcontainers | Medium | Per suite | High — same DB as prod |
| Shared test DB | Slow | Global | High — but flaky |

## Contract Testing

Verifies that a service provider and consumer agree on the API contract:

```
Consumer test:  "I expect GET /users/1 to return { id, name, email }"
Provider test:  "GET /users/1 actually returns { id, name, email }"
       ↓
Either side changes → contract breaks → caught before deploy
```

| Tool | Ecosystem | Use Case |
|------|-----------|----------|
| Pact | Multi-language | Consumer-driven contracts |
| Spring Cloud Contract | JVM | Provider-driven contracts |
| Postman/Schemas | OpenAPI | Schema-based contract validation |

## Best Practices

- **Test one integration at a time** — don't test the full stack in an integration test (that's E2E)
- **Clean state between tests** — reset databases, queues, and caches
- **Use realistic data** — not just happy path, include edge cases
- **Make them fast enough to run in CI** — < 1 minute per integration test file
- **Mark slow tests** — so they can be separated from the fast unit suite

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Testing everything as integration | Slow test suite | Use test pyramid — more unit, fewer integration |
| Shared database state | Flaky, order-dependent tests | Transaction-per-test or truncate between tests |
| Mocking the integration point | Tests pass, production fails | Use real DB/container, not a mock |
| No teardown | Stale data pollutes later tests | Always clean up in `afterEach`/teardown |

## What's Next?

Integration tests verify components work together. For full user journeys, move to [End-to-End Testing](end-to-end-testing.md).
