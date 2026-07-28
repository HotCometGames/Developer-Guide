# Design Patterns

> Reusable solutions to common software design problems — the shared vocabulary every developer should know.

> **Related:** [SOLID Principles](solid-principles.md) | [Hexagonal Architecture](hexagonal-architecture.md)

---

## What Are They?

Design patterns are **proven templates** for solving recurring design problems. They're not code you copy — they're recipes you adapt.

Three categories:

| Category | What It Does | Example |
|----------|-------------|---------|
| **Creational** | Controls object creation | Factory, Singleton, Builder |
| **Structural** | Composes objects into larger structures | Adapter, Facade, Decorator |
| **Behavioral** | Manages communication between objects | Observer, Strategy, Command |

---

## Creational Patterns

### Singleton

One instance, global access point.

```python
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

| Use When | Avoid When |
|----------|------------|
| Exactly one instance is needed (connection pool, logger) | It hides dependencies and makes testing hard |

> **Warning:** Singletons are often overused. Prefer dependency injection — pass a single instance explicitly rather than reaching for a global.

### Factory

Creates objects without specifying the exact class.

```python
class LoggerFactory:
    @staticmethod
    def create(log_type: str) -> Logger:
        if log_type == "file":
            return FileLogger()
        elif log_type == "console":
            return ConsoleLogger()
        else:
            raise ValueError(f"Unknown logger: {log_type}")
```

| Use When | Avoid When |
|----------|------------|
| Object creation logic is complex or conditional | A simple constructor call suffices |

### Builder

Constructs complex objects step by step.

```python
class QueryBuilder:
    def __init__(self):
        self._select = []
        self._from = ""
        self._where = []

    def select(self, *fields):
        self._select.extend(fields)
        return self

    def from_table(self, table: str):
        self._from = table
        return self

    def where(self, condition: str):
        self._where.append(condition)
        return self

    def build(self) -> str:
        return f"SELECT {', '.join(self._select)} FROM {self._from} WHERE {' AND '.join(self._where)}"

# Usage
query = QueryBuilder().select("name", "email").from_table("users").where("age > 18").build()
```

| Use When | Avoid When |
|----------|------------|
| An object requires many optional parameters | The object is simple (named params suffice) |

---

## Structural Patterns

### Adapter

Makes incompatible interfaces work together.

```python
# Third-party XML library (incompatible with our JSON system)
class XMLService:
    def get_xml_data(self): return "<data><item>1</item></data>"

# Our system expects JSON
class JSONAdapter:
    def __init__(self, xml_service: XMLService):
        self.xml_service = xml_service

    def get_data(self):
        xml = self.xml_service.get_xml_data()
        # Convert XML to JSON
        return {"items": ["1"]}
```

| Use When | Avoid When |
|----------|------------|
| You need to integrate an incompatible interface | You can change the target interface directly |

### Facade

Simplifies a complex subsystem behind a single easy-to-use interface.

```python
class ComputerFacade:
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.hard_drive = HardDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load("boot_address", self.hard_drive.read("boot_sector"))
        self.cpu.execute()
```

| Use When | Avoid When |
|----------|------------|
| You want to hide subsystem complexity from callers | The facade becomes a "god object" that knows too much |

### Decorator

Adds behavior to an object dynamically without changing its class.

```python
from functools import wraps

def log_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@log_calls
def add(a, b):
    return a + b
```

| Use When | Avoid When |
|----------|------------|
| You need to add cross-cutting behavior (logging, timing, caching) | The behavior is essential to the core logic, not an add-on |

---

## Behavioral Patterns

### Observer

One-to-many notification — when one object changes, all dependents are notified.

```python
class EventEmitter:
    def __init__(self):
        self._handlers = {}

    def on(self, event: str, handler):
        if event not in self._handlers:
            self._handlers[event] = []
        self._handlers[event].append(handler)

    def emit(self, event: str, *args):
        for handler in self._handlers.get(event, []):
            handler(*args)

# Usage
emitter = EventEmitter()
emitter.on("user_saved", lambda user: print(f"Saved {user.name}"))
emitter.on("user_saved", lambda user: send_welcome_email(user))
emitter.emit("user_saved", user)
```

| Use When | Avoid When |
|----------|------------|
| One event should trigger multiple independent actions | You need guaranteed ordering or synchronous responses |

### Strategy

Swaps algorithms at runtime.

```python
from abc import ABC, abstractmethod

class SortStrategy(ABC):
    @abstractmethod
    def sort(self, data): ...

class QuickSort(SortStrategy):
    def sort(self, data): ...

class MergeSort(SortStrategy):
    def sort(self, data): ...

class Sorter:
    def __init__(self, strategy: SortStrategy):
        self.strategy = strategy

    def sort(self, data):
        return self.strategy.sort(data)
```

| Use When | Avoid When |
|----------|------------|
| You have multiple algorithms that differ only in behavior | A simple if/else or switch is enough |

### Command

Encapsulates a request as an object, enabling undo/redo, queuing, and logging.

```python
from abc import ABC, abstractmethod

class Command(ABC):
    @abstractmethod
    def execute(self): ...
    @abstractmethod
    def undo(self): ...

class AddTextCommand(Command):
    def __init__(self, doc, text):
        self.doc = doc
        self.text = text

    def execute(self):
        self.doc.add(self.text)

    def undo(self):
        self.doc.remove(self.text)

# Usage
history = []
cmd = AddTextCommand(document, "Hello")
cmd.execute()
history.append(cmd)
# Later: history.pop().undo()
```

| Use When | Avoid When |
|----------|------------|
| You need undo/redo, task queues, or operation logging | The operation is fire-and-forget with no need to reverse |

---

## Cheat Sheet

| Pattern | Type | Problem It Solves |
|---------|------|-------------------|
| Singleton | Creational | Single instance, global access |
| Factory | Creational | Conditional object creation |
| Builder | Creational | Complex object construction |
| Adapter | Structural | Interface incompatibility |
| Facade | Structural | Complex subsystem |
| Decorator | Structural | Dynamic behavior extension |
| Observer | Behavioral | One-to-many notifications |
| Strategy | Behavioral | Swappable algorithms |
| Command | Behavioral | Encapsulated actions, undo |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Pattern overuse | Solving simple problems with complex patterns | Start with simple code, refactor toward a pattern when you need it |
| Misapplying patterns | Using a pattern because it's "cool" | Let the problem drive the pattern choice |
| Ignoring language features | Using Command pattern when Python has first-class functions | Use the simplest tool: functions, closures, or callbacks first |

## Related Topics

- [SOLID Principles](solid-principles.md) — Patterns uphold SOLID principles
- [Hexagonal Architecture](hexagonal-architecture.md) — Structural patterns applied at system scale

## Further Learning

- *Design Patterns: Elements of Reusable Object-Oriented Software* — The "Gang of Four" book
- *Head First Design Patterns* — More accessible introduction

---

> **Next:** [Architecture Styles](architecture-styles.md) | **Previous:** [SOLID Principles](solid-principles.md)
