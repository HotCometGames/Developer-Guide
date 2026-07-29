# Debugging Mindset

> A systematic approach to finding and fixing bugs — without the frustration.

> **Related:** [Code Smells & Refactoring](code-smells-and-refactoring.md) | [Troubleshooting](troubleshooting.md)

---

## What Is It?

Debugging is the art of figuring out why code doesn't behave as expected. The best debuggers follow a methodical process rather than guessing randomly.

## The Debugging Process

```
1. Reproduce the bug consistently
2. Understand the expected behavior
3. Understand the actual behavior
4. Narrow down the scope (bisect)
5. Form a hypothesis
6. Test the hypothesis
7. Fix the root cause
8. Add a regression test
```

### 1. Reproduce

If you can't reproduce it, you can't fix it.

- Find the exact steps, inputs, and conditions
- If it's intermittent, look for timing, race conditions, or uninitialized state
- Write a test that reproduces the bug

### 2. Understand Expected vs Actual

```
Expected:  Function returns the user's name
Actual:    Function returns null for users named "Null"
```

What's the gap? What assumption is wrong?

### 3. Narrow the Scope — Binary Search

```
Source of bug is somewhere in a 1000-line request handler:

1. Is it before or after line 500?   → After
2. Is it before or after line 750?   → Before
3. Line 625?                         → Found it!
```

Apply this to code, git history (`git bisect`), and data:

```bash
git bisect start
git bisect bad HEAD        # current commit is broken
git bisect good v1.0       # v1.0 was working
# Git checks out the midpoint → you test → git bisect good/bad
# Repeat until the bad commit is identified
```

### 4. Form a Hypothesis

A good hypothesis is specific and testable:

| Bad | Good |
|-----|------|
| "Something is wrong with the payment code" | "The payment fails when the amount includes cents because the API expects integers" |
| "It might be a caching issue" | "The cache key doesn't include the user ID, so user A sees user B's data" |

### 5. Test the Hypothesis

Add a print/log, write a unit test, add an assertion, or use a debugger. One change at a time.

### 6. Fix the Root Cause

Fix the cause, not the symptom:

```python
# Symptom fix — hides the problem
try:
    process(data)
except:
    pass

# Root cause fix — addresses why it failed
def process(data):
    if not data.is_valid:
        raise ValueError(f"Invalid data: {data}")
    # ... actual processing
```

### 7. Add a Regression Test

```python
def test_edge_case_that_caused_the_bug():
    with pytest.raises(ValueError):
        process(invalid_data)
```

## Rubber Duck Debugging

Explain the problem to someone — or something (a rubber duck, a text editor, your terminal). The act of describing the problem often reveals the solution.

```
You: "The function should return the total, but it returns 0..."
You: "Wait, I see it — I'm resetting the accumulator on every iteration."
```

## Debugging Tools

| Tool | When |
|------|------|
| `print()` / logging | Quick checks, server-side debugging |
| Debugger (breakpoints) | Complex control flow, inspecting state |
| `git bisect` | Finding which commit introduced the bug |
| `diff` inputs | Data-dependent bugs (compare working vs failing input) |
| Stress testing | Race conditions, memory bugs |

## Common Mental Traps

| Trap | What It Looks Like | How to Escape |
|------|--------------------|---------------|
| Confirmation bias | Looking for evidence that supports your theory | Try to prove yourself wrong instead |
| Cargo cult fix | Applying a fix you don't understand | Understand the root cause first |
| "It can't be X" | Dismissing a possibility without checking | Check anyway — eliminate possibilities systematically |
| Too many variables | Changing multiple things at once | One change, test, repeat |
| Sunk cost | Hours invested, can't step back | Take a break, explain to someone else |

## Best Practices

- **Read the error message** — fully, including the stack trace — before doing anything else
- **Check recent changes first** — most bugs are introduced by the last change
- **Make it fail faster** — if a bug takes 5 minutes to reproduce, find a way to reproduce it in 5 seconds
- **Keep a debug log** — write down what you tried, what happened, and what you concluded
- **Know when to ask for help** — if 30 minutes of systematic debugging fails, explain it to someone

## What's Next?

Prevent future debugging sessions with solid [Engineering Principles](engineering-principles.md) and clean code.
