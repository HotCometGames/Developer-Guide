# Architecture Troubleshooting

> Common architectural anti-patterns, their symptoms, and how to fix them.

> **Related:** [What Is Software Architecture?](what-is-software-architecture.md) | [SOLID Principles](solid-principles.md) | [Architecture Styles](architecture-styles.md)

---

## How to Diagnose Architecture Problems

Before jumping to fix architecture problems, **measure**. Symptoms that look like "scalability" are often "bad query" problems. Symptoms that look like "maintainability" are often "no tests" problems.

Ask these questions:

1. **What specifically hurts?** — Slow deploys? Bugs on every change? Hard to onboard?
2. **Where does the pain live?** — One module? One service? The build process?
3. **When did it start?** — After a specific change? After the team grew?
4. **What happens if we don't fix it?** — Is it getting worse?

If the answer is "it's annoying but we're shipping fine", fix it incrementally. If the answer is "we're losing customers", prioritize the fix.

---

## Anti-Pattern: Big Ball of Mud

> A system with no clear structure — everything depends on everything.

**Symptoms:**
- Changing one thing breaks something unrelated
- Developers are afraid to refactor
- "This code is a mess" is a common complaint
- No clear module boundaries

**Root cause:**
- No architecture from the start
- Shortcuts that became permanent
- No enforcement of boundaries

**How to fix:**
1. **Identify the seams** — Find natural boundaries in the code (by feature, by domain concept)
2. **Draw lines** — Define interfaces between modules
3. **Extract incrementally** — Move one module at a time behind its interface
4. **Enforce** — Use linters, architecture tests, or code reviews to prevent new violations

```python
# Before — everything imported everywhere
from models import User
from utils import send_email
from services import payment
from helpers import format_date
from config import settings
from legacy import whatever

# After — clear boundaries
from billing.domain.models import User
from billing.infrastructure.email import send_email
from billing.use_cases.process_payment import PaymentProcessor
```

---

## Anti-Pattern: God Class

> A single class that does everything — validation, persistence, email, logging, orchestration.

**Symptoms:**
- A class with hundreds or thousands of lines
- The class has 10+ responsibilities
- Every feature requires changes to this class
- The class can't be tested without mocking 15 dependencies

**Root cause:**
- Violation of Single Responsibility Principle
- "I'll put it here for now" repeated 50 times

**How to fix:**
1. **List every responsibility** — Write down everything the class does
2. **Group into focused classes** — Each responsibility becomes its own class
3. **Collaborate, don't control** — The original class becomes a coordinator that delegates to the new classes

---

## Anti-Pattern: Premature Abstraction

> Abstracting for "future flexibility" when the future is unknown — resulting in complex, hard-to-follow code that doesn't solve a real problem.

**Symptoms:**
- Deep inheritance hierarchies with one concrete implementation
- Strategy/Factory/Template patterns applied to simple problems
- "We might need this later" in code reviews
- Adding a new feature requires touching 5 files

**Root cause:**
- Applying patterns before understanding the problem
- Over-engineering in the name of "good design"

**How to fix:**
1. **Start concrete** — Write the simplest thing that works
2. **Wait for duplication** — Apply the Rule of Three: wait until you see the same pattern three times before abstracting
3. **Refactor toward the pattern** — Extract abstractions when the concrete code becomes painful

> **Remember:** `yagni — You Aren't Gonna Need It. Solve today's problem well. Tomorrow's problem will be clearer tomorrow.

---

## Anti-Pattern: Distributed Monolith

> A system deployed as microservices but tightly coupled like a monolith — the worst of both worlds.

**Symptoms:**
- Changing one service requires deploying 3 others
- Services share a database
- Synchronous calls between services for every operation
- "Microservices" but the team still coordinates every release

**Root cause:**
- Splitting by technical layer (frontend, backend, database) instead of by business capability
- Shared database instead of database-per-service
- No bounded context mapping

**How to fix:**
1. **Database-per-service** — Each service owns its data
2. **Async where possible** — Use events instead of synchronous calls
3. **Define service boundaries** — Group related functionality, split unrelated
4. **Tolerate duplication** — Don't share code between services; duplication is cheaper than coupling

---

## Anti-Pattern: Golden Hammer

> Every problem looks like a nail because you have a favorite pattern — event sourcing for a blog, microservices for a todo app, a new framework for every service.

**Symptoms:**
- Overly complex solutions to simple problems
- "We use [pattern] for everything"
- High friction for simple changes

**Root cause:**
- Treating architecture as fashion rather than tradeoffs
- Technology-first thinking over problem-first thinking

**How to fix:**
1. **Start with the simplest correct answer** — A monolith with modular code solves 90% of problems
2. **Question the "why"** — "This pattern solves X. Do we have X?"
3. **Match complexity to problem** — Simple problems get simple solutions

---

## Anti-Pattern: Analysis Paralysis

> Spending so much time designing the architecture that nothing gets built.

**Symptoms:**
- Architecture diagrams but no running code
- "We need to finalize the design" for months
- Perfect solutions that never ship
- Decision-making takes weeks

**Root cause:**
- Fear of making the wrong decision
- Treating architecture as a one-time design rather than an evolving structure

**How to fix:**
1. **Set a deadline** — Architecture decisions get 2 hours, not 2 weeks
2. **Document tradeoffs** — Write an ADR explaining the choice, not trying to find the perfect choice
3. **Build a spike** — Prove the architecture with running code, not diagrams
4. **Iterate** — The first architecture won't be the last. That's OK.

---

## Quick Reference

| Anti-Pattern | Primary Symptom | Quick Fix |
|-------------|----------------|-----------|
| Big Ball of Mud | Everything depends on everything | Draw module boundaries, extract incrementally |
| God Class | 1000-line class doing everything | One responsibility per class |
| Premature Abstraction | Pattern soup, no clear benefit | Start concrete, abstract when needed |
| Distributed Monolith | Microservices that must be deployed together | Database-per-service, async communication |
| Golden Hammer | Same pattern for every problem | Match solution complexity to problem |
| Analysis Paralysis | Architecture never ships | Set deadlines, write ADRs, build spikes |

## Related Topics

- [What Is Software Architecture?](what-is-software-architecture.md) — Architectural thinking
- [SOLID Principles](solid-principles.md) — The fundamentals of clean design
- [Architecture Styles](architecture-styles.md) — Choosing the right style

## Further Learning

- *Refactoring: Improving the Design of Existing Code* — Martin Fowler
- *Working Effectively with Legacy Code* — Michael Feathers
- *The Pragmatic Programmer* — Hunt & Thomas (especially "Don't Live with Broken Windows")

---

> **Previous:** [Scalability Patterns](scalability-patterns.md) | **Next:** [Project Management](../11-project-management/README.md)
