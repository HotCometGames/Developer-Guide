# SOLID Principles

> Five design principles for writing maintainable, understandable, and flexible object-oriented code.

> **Related:** [Design Patterns](design-patterns.md) | [What Is Software Architecture?](what-is-software-architecture.md)

---

## What Are They?

SOLID is an acronym for five principles introduced by Robert C. Martin:

| Letter | Principle | Core Idea |
|--------|-----------|-----------|
| **S** | Single Responsibility | One class = one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subtypes must be substitutable for their base types |
| **I** | Interface Segregation | Many small interfaces > one fat interface |
| **D** | Dependency Inversion | Depend on abstractions, not concretions |

---

## S — Single Responsibility Principle

> A class should have only one reason to change.

**Violation:**

```python
class OrderService:
    def create_order(self, items):
        # 1. Validates items
        # 2. Calculates total
        # 3. Saves to database
        # 4. Sends email confirmation
        # 5. Logs to analytics
        pass
```

**Fix — split into focused classes:**

```python
class OrderValidator:
    def validate(self, items): ...

class OrderCalculator:
    def calculate(self, items): ...

class OrderRepository:
    def save(self, order): ...

class EmailService:
    def send_confirmation(self, order): ...

class AnalyticsService:
    def track_order(self, order): ...
```

> **Tip:** If you can't describe what a class does without saying "and", it's probably doing too much.

## O — Open/Closed Principle

> Classes should be open for extension but closed for modification.

**Violation:**

```python
class PaymentProcessor:
    def process(self, payment_type: str):
        if payment_type == "credit_card":
            # process credit card
        elif payment_type == "paypal":
            # process paypal
        # Adding a new type means modifying this class
```

**Fix — use polymorphism:**

```python
from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def process(self): ...

class CreditCard(PaymentMethod):
    def process(self): ...

class PayPal(PaymentMethod):
    def process(self): ...

class PaymentProcessor:
    def process(self, method: PaymentMethod):
        method.process()
```

Now adding a new payment type means creating a new class — no existing code changes.

## L — Liskov Substitution Principle

> If you have a function that takes a base class, you should be able to pass any subclass without the function breaking.

**Violation:**

```python
class Rectangle:
    def __init__(self):
        self.width = 0
        self.height = 0

    def set_width(self, w): self.width = w
    def set_height(self, h): self.height = h
    def area(self): return self.width * self.height

class Square(Rectangle):
    def set_width(self, w):
        self.width = w
        self.height = w  # Violates LSP!

    def set_height(self, h):
        self.height = h
        self.width = h    # Violates LSP!
```

A function like `make_big(rect: Rectangle)` that calls `rect.set_width(5); rect.set_height(10)` and expects `rect.area() == 50` would break with a `Square`.

**Fix:** Don't model `Square` as a subclass of `Rectangle`. Use a common abstract `Shape`:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w, self.h = w, h
    def area(self): return self.w * self.h

class Square(Shape):
    def __init__(self, side):
        self.side = side
    def area(self): return self.side ** 2
```

> **Remember:** Inheritance is not for code reuse — it's for substitutability.

## I — Interface Segregation Principle

> No client should be forced to depend on methods it doesn't use.

**Violation:**

```python
class IWorker(ABC):
    @abstractmethod
    def work(self): ...
    @abstractmethod
    def eat(self): ...
    @abstractmethod
    def sleep(self): ...

class Robot(IWorker):
    def work(self): ...
    def eat(self): raise NotImplementedError  # Robots don't eat
    def sleep(self): raise NotImplementedError  # Robots don't sleep
```

**Fix — split into small interfaces:**

```python
class IWorkable(ABC):
    @abstractmethod
    def work(self): ...

class IFeedable(ABC):
    @abstractmethod
    def eat(self): ...

class IRestable(ABC):
    @abstractmethod
    def sleep(self): ...

class Human(IWorkable, IFeedable, IRestable):
    def work(self): ...
    def eat(self): ...
    def sleep(self): ...

class Robot(IWorkable):
    def work(self): ...
```

> **Tip:** If implementing an interface forces you to write `raise NotImplementedError`, you've violated ISP.

## D — Dependency Inversion Principle

> High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Violation:**

```python
class MySQLDatabase:
    def save(self, data):
        # save to MySQL

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()  # Tight coupling
```

**Fix — depend on an abstraction:**

```python
from abc import ABC, abstractmethod

class IDatabase(ABC):
    @abstractmethod
    def save(self, data): ...

class MySQLDatabase(IDatabase):
    def save(self, data): ...

class PostgreSQLDatabase(IDatabase):
    def save(self, data): ...

class UserService:
    def __init__(self, db: IDatabase):  # Abstraction injected
        self.db = db
```

Now `UserService` doesn't care what database is used. You could swap MySQL for PostgreSQL without changing a line in `UserService`.

---

## Cheat Sheet

| Principle | Quick Check |
|-----------|-------------|
| SRP | Can I describe this class in one sentence? |
| OCP | Can I add a new feature without editing existing classes? |
| LSP | Would a subclass break code that uses the base class? |
| ISP | Am I forcing clients to depend on methods they don't use? |
| DIP | Do my high-level modules depend on interfaces, not implementations? |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Applying SRP too aggressively | Class explosion, too many tiny files | Group related behavior, split only when you have multiple reasons to change |
| OCP via inheritance only | Deep, brittle class hierarchies | Use composition + interfaces instead |
| Ignoring LSP | Runtime bugs that are hard to trace | Think "is-a" vs "works-like-a" |
| One giant interface | Every change forces recompilation of all implementors | Keep interfaces focused |
| DIP with new keyword everywhere | Hard to test, impossible to swap | Use constructor injection |

## Related Topics

- [Design Patterns](design-patterns.md) — Many patterns exist to uphold SOLID
- [Dependency Injection](dependency-injection.md) — DIP in practice
- [What Is Software Architecture?](what-is-software-architecture.md) — Where SOLID fits in the big picture

## Further Learning

- *Clean Code* — Robert C. Martin
- *Agile Software Development, Principles, Patterns, and Practices* — Robert C. Martin

---

> **Next:** [Design Patterns](design-patterns.md) | **Previous:** [What Is Software Architecture?](what-is-software-architecture.md)
