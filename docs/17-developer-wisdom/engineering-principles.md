# Engineering Principles

> KISS, YAGNI, DRY, SoC — the four pillars of practical software design.

> **Related:** [Code Smells & Refactoring](code-smells-and-refactoring.md) | [Decision Making & Trade-offs](decision-making-and-tradeoffs.md)

---

## KISS — Keep It Simple, Stupid

> Simplicity is the ultimate sophistication.

| Principle | Instead of | Do |
|-----------|------------|-----|
| Simple over clever | One-liner with three side effects | Readable multi-step code |
| Obvious over fast | Complex optimized code | Clear code, optimize when profiled |
| Minimal over flexible | Generic framework for one use case | Specific solution to the problem at hand |

```python
# Avoid
result = [x for xs in matrix for x in xs if x is not None][:5]

# Prefer
flat = []
for row in matrix:
    for item in row:
        if item is not None:
            flat.append(item)
            if len(flat) == 5:
                break
    if len(flat) == 5:
        break
result = flat
```

> **Note:** "Simple" means easy to understand and change, not necessarily few lines.

## YAGNI — You Aren't Gonna Need It

> Build what you need now, not what you might need someday.

```python
# Avoid — speculative abstraction
class PaymentProcessor:
    def process(self, payment, gateway=None):
        # What if we need Stripe? Square? PayPal? Let me abstract now...
        ...

# Prefer — concrete, then refactor when a second gateway appears
def process_stripe_payment(payment):
    ...
```

| Pattern | YAGNI Violation | Better Approach |
|---------|----------------|-----------------|
| Configuration files with flags for features that don't exist | Premature flexibility | Add config when you have a second use case |
| Abstract factory for one implementation | Over-engineering | Concrete class, extract interface when needed |
| Database schema with columns for "future features" | Dead columns | Add columns when features are built |

## DRY — Don't Repeat Yourself

> Every piece of knowledge should have a single, unambiguous representation.

```python
# Avoid — duplicated logic
def calculate_discount_regular(price):
    if price > 100:
        return price * 0.9
    return price

def calculate_discount_vip(price):
    if price > 100:
        return price * 0.8
    return price

# Prefer — single source of truth
def calculate_discount(price, discount_rate):
    if price > 100:
        return price * discount_rate
    return price
```

> **Warning:** DRY doesn't mean "remove all duplication regardless." Two things that happen to look the same but change for different reasons should stay separate.

## SoC — Separation of Concerns

> Each module, class, or function should have one job and one reason to change.

```python
# Avoid — mixed concerns
def process_order(order):
    db.save(order)                        # persistence
    send_email(order)                     # notification
    log_to_sentry(f"Order {order.id}")    # logging
    update_inventory(order)               # inventory
    return {"status": "ok"}               # HTTP response

# Prefer — separated concerns
class OrderProcessor:
    def __init__(self, order_repo, notifier, logger):
        self.order_repo = order_repo
        self.notifier = notifier
        self.logger = logger

    def process(self, order):
        self.order_repo.save(order)
        self.notifier.send_confirmation(order)
        self.logger.info(f"Order {order.id} processed")
```

| Concern | Responsibility | When to Separate |
|---------|---------------|------------------|
| Data access | Reading/writing to storage | Different from business logic |
| HTTP handling | Request/response, status codes | Different from business logic |
| Business logic | Domain rules | The core of your app — keep it pure |
| Logging | Observability | Cross-cutting concern (aspect) |
| Configuration | Environment-specific settings | Separate from application code |

## When Principles Conflict

| Conflict | Resolution |
|----------|------------|
| DRY vs KISS | A little duplication is better than a fragile abstraction |
| YAGNI vs SoC | Don't pre-extract concerns, but don't put everything in one function either |
| DRY vs Performance | Cache the result instead of recomputing; keep the single source of truth |

## What's Next?

Apply these principles by recognizing [Code Smells & Refactoring](code-smells-and-refactoring.md) opportunities.
