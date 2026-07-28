# Dependency Injection

> A technique where an object receives its dependencies from the outside rather than creating them itself — the foundation of testable, loosely coupled code.

> **Related:** [SOLID Principles](solid-principles.md) | [Hexagonal Architecture](hexagonal-architecture.md) | [Design Patterns](design-patterns.md)

---

## What Is It?

Dependency Injection (DI) is the **"D" in SOLID** (Dependency Inversion) in practice. Instead of a class creating its own dependencies:

```python
# Without DI
class OrderService:
    def __init__(self):
        self.logger = FileLogger()  # Hard-coded dependency
        self.db = MySQLDatabase()   # Hard-coded dependency
```

You **inject** them:

```python
# With DI
class OrderService:
    def __init__(self, logger: Logger, db: Database):
        self.logger = logger  # Injected from outside
        self.db = db          # Injected from outside
```

## Why Does It Exist?

| Without DI | With DI |
|-----------|---------|
| Hard to test — needs real database | Easy to test — pass mocks or fakes |
| Impossible to swap implementations | Swap by passing a different object |
| Hidden dependencies — unclear what a class needs | Dependencies are explicit in the constructor |
| Tight coupling — changes ripple everywhere | Loose coupling — classes depend on abstractions |

## Mental Model

Think of your application as a **tree of objects**:

```
Application
 ├── UserController
 │    ├── UserService
 │    │    ├── UserRepository (interface)
 │    │    │    ├── MySQLUserRepository (concrete)
 │    │    └── EmailService (interface)
 │    │         └── SendGridEmailService (concrete)
 │    └── Logger (interface)
 │         └── ConsoleLogger (concrete)
 └── HealthController
      └── Logger (same instance)
```

Without DI, every object constructs its own tree. With DI, the **composition root** (usually `main.py` or a DI container) builds the entire tree at startup.

## Three Forms of Injection

### 1. Constructor Injection (Preferred)

```python
class UserService:
    def __init__(self, repo: UserRepository, email: EmailService):
        self.repo = repo
        self.email = email

    def register(self, name: str, email: str):
        user = User(name, email)
        self.repo.save(user)
        self.email.send_welcome(user)
        return user
```

| Pros | Cons |
|------|------|
| Dependencies are explicit and required | Can become verbose with many dependencies |
| Immutable — set once, never changed | |
| Works with any DI container | |

### 2. Setter Injection

```python
class UserService:
    def set_repository(self, repo: UserRepository):
        self.repo = repo

    def set_email_service(self, email: EmailService):
        self.email = email
```

| Pros | Cons |
|------|------|
| Optional dependencies | Object can be used before dependencies are set |
| Allows reconfiguration | Not clear what's required vs optional |

### 3. Method Injection

```python
class UserService:
    def register(self, name: str, email: str, repo: UserRepository):
        user = User(name, email)
        repo.save(user)
        return user
```

| Pros | Cons |
|------|------|
| Dependency only needed for one method | Awkward if multiple methods need the same dependency |
| No constructor pollution | Caller must know about the dependency |

> **Recommendation:** Use constructor injection by default. Use setter injection for optional dependencies. Use method injection when the dependency varies per call.

## DI Containers

A DI container automates wiring. Instead of manually constructing the tree, you **register** types and the container resolves them.

### Example: `dependency_injector` (Python)

```python
from dependency_injector import containers, providers

class Container(containers.DeclarativeContainer):
    config = providers.Configuration()

    # Database
    db = providers.Singleton(MySQLDatabase, host=config.db.host)

    # Repositories
    user_repo = providers.Factory(MySQLUserRepository, db=db)

    # Services
    email_service = providers.Factory(SendGridEmailService, api_key=config.sendgrid.api_key)
    user_service = providers.Factory(UserService, repo=user_repo, email=email_service)
```

Then in your composition root:

```python
container = Container()
container.config.db.host.from_env("DB_HOST")
container.config.sendgrid.api_key.from_env("SENDGRID_KEY")

app = Flask(__name__)
app.user_service = container.user_service()  # Fully wired UserService
```

### Example: Manual Wiring (No Container)

```python
# main.py — composition root
def create_app():
    db = MySQLDatabase(host=os.environ["DB_HOST"])
    user_repo = MySQLUserRepository(db)
    email_svc = SendGridEmailService(os.environ["SENDGRID_KEY"])
    user_service = UserService(user_repo, email_svc)
    controller = UserController(user_service)
    return FlaskApp(controller)
```

> **Tip:** You don't need a DI container. Manual wiring in your composition root works perfectly fine for small to medium applications. Add a container when wiring becomes painful.

## Service Locator (Anti-Pattern)

```python
# Anti-pattern
class ServiceLocator:
    _services = {}

    @classmethod
    def register(cls, key, instance):
        cls._services[key] = instance

    @classmethod
    def get(cls, key):
        return cls._services[key]

# Usage — hides dependencies
class OrderService:
    def __init__(self):
        self.db = ServiceLocator.get("database")  # Hidden dependency!
```

**Why it's bad:**

- Dependencies are **hidden** — you can't tell what a class needs by looking at its constructor
- Testing is harder — you must configure the global locator before each test
- **Implicit coupling** — any class can reach into the locator for anything
- Ruby on Rails popularized this pattern; most frameworks have moved away from it

## When Should I Use DI?

| Use When | Don't Use When |
|----------|---------------|
| The dependency might change (DB, API, email) | The dependency is a pure utility (math helper) |
| You want to unit test the class | The class has no logic worth testing |
| The dependency is external (network, filesystem) | The dependency is in the same module and never changes |
| Following hexagonal architecture | Prototype code that will be rewritten |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Over-injecting everything | Constructor takes 15 parameters | Group related dependencies into value objects or facades |
| Using service locator | Hidden dependencies, testing pain | Use constructor injection |
| Injecting primitives | Confusing — what does `host`, `port` mean? | Inject configuration objects |
| Not using a composition root | Wiring sprinkled through the codebase | Wire everything in one place |
| Container everywhere | Framework coupling — can't easily swap | Container only touches composition root |

## Related Topics

- [SOLID Principles](solid-principles.md) — DI is the application of DIP + LSP
- [Hexagonal Architecture](hexagonal-architecture.md) — DI is how ports are wired to adapters
- [Design Patterns](design-patterns.md) — Factory pattern is a close relative

## Further Learning

- *Dependency Injection in .NET* — Mark Seemann
- *Clean Architecture* — Robert C. Martin

---

> **Next:** [Architecture Decision Records](architecture-decision-records.md) | **Previous:** [API Design](api-design.md)
