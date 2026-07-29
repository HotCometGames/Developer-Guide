# Code Smells & Refactoring

> Recognizing when code is trying to tell you something — and how to improve it safely.

> **Related:** [Engineering Principles](engineering-principles.md) | [Debugging Mindset](debugging-mindset.md)

---

## What Is It?

A code smell is a surface-level symptom that usually indicates a deeper problem. It's not a bug — the code works — but it suggests the design could be improved.

## Common Code Smells

### Long Method

Anything over 20 lines deserves scrutiny. Over 50 lines, extract.

```python
# Smell
def process_order(order, user, inventory, payment_gateway):
    # validate user
    if not user.is_active:
        raise ValueError("Inactive user")
    if user.balance < order.total:
        raise ValueError("Insufficient funds")
    # check inventory (10 more lines)
    # process payment (15 more lines)
    # update inventory (8 more lines)
    # send notification (12 more lines)
    # log (3 more lines)
    # return response (5 more lines)

# Better
def process_order(order, user, inventory, payment_gateway):
    _validate_user(user, order)
    _check_inventory(inventory, order.items)
    payment = _process_payment(payment_gateway, order)
    _update_inventory(inventory, order.items)
    _send_confirmation(user, order)
    _log_order(order, payment)
    return _build_response(order, payment)
```

### God Class

One class that does everything. Split by responsibility.

| Symptom | Fix |
|---------|-----|
| Class has "and" in its description | Split into separate classes |
| Class has 20+ methods | Group related methods into new classes |
| Class imports from 10+ modules | Import surface indicates too many responsibilities |

### Primitive Obsession

Using primitive types where a value object would make intent clear:

```python
# Smell
def create_user(email: str, role: str, status: str):
    ...

# Better
@dataclass
class Email:
    address: str
    def __post_init__(self):
        assert "@" in self.address

@dataclass
class Role:
    name: str  # "admin", "user", "moderator"

@dataclass
class UserStatus:
    value: str  # "active", "inactive", "suspended"

def create_user(email: Email, role: Role, status: UserStatus):
    ...
```

### Feature Envy

A method that uses another class's data more than its own:

```python
# Smell — OrderLine calculates, but uses Product's data
class OrderLine:
    def calculate_price(self):
        return self.quantity * self.product.price * (1 - self.product.discount)

# Better — let Product calculate its own contribution
class Product:
    def price_for_quantity(self, quantity):
        return quantity * self.price * (1 - self.discount)

class OrderLine:
    def calculate_price(self):
        return self.product.price_for_quantity(self.quantity)
```

## Refactoring Workflow

```
1. Ensure tests exist          (safety net)
2. Identify the smell          (what's wrong?)
3. Choose one refactoring      (smallest change)
4. Apply refactoring           (change code)
5. Run tests                   (did it break?)
6. Commit                      (save progress)
7. Repeat                      (next smell)
```

## Key Refactorings

| Technique | When | How |
|-----------|------|-----|
| Extract Method | Long function | Pull code into named function |
| Rename Variable/Function | Unclear naming | Change to descriptive name |
| Inline Method | Unnecessary indirection | Replace call with body |
| Move Method | Wrong location | Move to appropriate class |
| Extract Class | Mixed responsibilities | Split into two classes |
| Introduce Parameter Object | Long parameter list | Wrap params in object |
| Replace Conditional with Polymorphism | Long if/else chain | Subclasses or strategy pattern |
| Decompose Conditional | Complex if/else | Extract conditions into functions |

## When NOT to Refactor

| Situation | Do Instead |
|-----------|------------|
| Code is working and never changes | Leave it |
| No tests exist | Add tests first, then refactor |
| You're in a hurry | Flag it, come back later |
| The module is scheduled for rewrite | Leave it, rewrite from scratch |
| You don't understand the code | Understand it first, then refactor |

## Best Practices

- **Refactor in small steps** — one change, test, commit, repeat
- **Separate refactoring from feature work** — different commits, ideally different PRs
- **Run tests after every refactoring** — if a test fails, you know exactly which change broke it
- **Use IDE refactoring tools** — automated rename, extract method, move are less error-prone
- **Delete dead code** — commented-out code, unused imports, unreachable branches

## What's Next?

Combine these patterns with a [Debugging Mindset](debugging-mindset.md) for systematic problem solving.
