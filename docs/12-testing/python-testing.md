# Python Testing

> pytest patterns, fixtures, markers, and configuration for testing Python projects.

> **Related:** [Unit Testing](unit-testing.md) | [Integration Testing](integration-testing.md) | [JavaScript Testing](javascript-testing.md)

---

## What Is It?

Python's testing ecosystem centers on **pytest** — a mature, extensible test runner with rich fixture support, powerful assertion introspection, and a large plugin ecosystem.

## Setup

```bash
pip install pytest pytest-cov
```

```ini
# pytest.ini
[pytest]
testpaths = tests
python_files = test_*.py
addopts = -v --cov=src --cov-report=term-missing
markers =
    slow: marks tests as slow (deselect with -m "not slow")
    integration: marks integration tests
```

## Fixtures

Fixtures are pytest's mechanism for setup and teardown. They can be scoped by function, class, module, or session.

```python
import pytest
from myapp import create_app, get_db

# Basic fixture
@pytest.fixture
def app():
    return create_app(testing=True)

# Scoped fixture — runs once per module
@pytest.fixture(scope="module")
def db():
    database = get_db(":memory:")
    database.migrate()
    yield database
    database.close()

# Autouse — applies to every test automatically
@pytest.fixture(autouse=True)
def setup_env():
    os.environ["APP_ENV"] = "testing"
    yield
    os.environ.pop("APP_ENV", None)

# Using fixtures
def test_create_user(app, db):
    user = app.create_user("alice@example.com")
    assert user.email == "alice@example.com"
    assert db.find_user(user.id) is not None
```

### conftest.py

Fixtures defined in `conftest.py` are automatically available to all tests in that directory and its subdirectories:

```python
# tests/conftest.py
@pytest.fixture
def client(app):
    return app.test_client()
```

```
tests/
├── conftest.py          ← shared fixtures (client, db, app)
├── test_auth.py         ← uses client, db from conftest
└── api/
    ├── conftest.py      ← fixtures specific to API tests
    └── test_users.py    ← uses both conftest files
```

## Parametrize

```python
@pytest.mark.parametrize("email,expected", [
    ("user@example.com", True),
    ("not-an-email", False),
    ("", False),
])
def test_email_validation(email, expected):
    assert is_valid_email(email) == expected
```

## Markers

| Marker | Purpose |
|--------|---------|
| `@pytest.mark.skip` | Always skip |
| `@pytest.mark.skipif(cond)` | Conditional skip |
| `@pytest.mark.xfail` | Expected to fail |
| `@pytest.mark.parametrize` | Run with multiple inputs |
| `@pytest.mark.slow` | Custom — run `-m "not slow"` to skip |

```bash
pytest -v                    # verbose
pytest -x                    # stop on first failure
pytest -k "create"           # run tests matching "create"
pytest -m "not slow"         # skip slow tests
pytest --lf                  # run last failed
pytest --ff                  # run failed first, then rest
```

## Mocking

```python
from unittest.mock import patch

def test_send_welcome_email():
    with patch("myapp.email.send") as mock_send:
        mock_send.return_value = {"status": "sent"}
        result = send_welcome_email("alice@example.com")
        mock_send.assert_called_once_with(
            "alice@example.com", subject="Welcome!"
        )
```

## Fixture Patterns

| Pattern | When | Example |
|---------|------|---------|
| Factory as fixture | Need variation | `def make_user(name): ...` |
| `tmp_path` | Temp files | Built-in pytest fixture |
| `monkeypatch` | Environment/import patching | `monkeypatch.setenv("KEY", "val")` |
| `capsys` | Capture stdout/stderr | `capsys.readouterr()` |

## Best Practices

- **Put fixtures in conftest.py** — share them across test files
- **Use fixture scoping** — `session` for DB connections, `function` for mutable state
- **Use `tmp_path` instead of manual temp dirs** — pytest cleans them up
- **Write parametrized tests** instead of looping in a single test
- **Run tests in parallel** — `pip install pytest-xdist` → `pytest -n auto`

## What's Next?

Apply these patterns with [Unit Testing](unit-testing.md) fundamentals, or learn the [JavaScript Testing](javascript-testing.md) equivalents for Node projects.
