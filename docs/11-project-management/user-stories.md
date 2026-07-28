# User Stories

> A lightweight way to describe features from the user's perspective — focused on value, not implementation.

> **Related:** [Estimation & Planning](estimation-and-planning.md) | [Scrum](scrum.md)

---

## What Is It?

A user story is a **short, simple description of a feature** told from the perspective of the person who wants it. It shifts the conversation from "what should the system do" to "what does the user need to accomplish."

## Standard Format

```
As a [user role],
I want [goal],
So that [benefit].
```

### Examples

```
As a logged-in user,
I want to reset my password,
So that I can regain access if I forget it.

As an admin,
I want to see a list of recent sign-ups,
So that I can monitor account growth.

As a customer,
I want to receive an order confirmation email,
So that I have a record of my purchase.
```

> **Tip:** If you can't write the "so that" part clearly, you don't understand why the feature exists. Go talk to the user.

## The INVEST Criteria

| Letter | Meaning | Check |
|--------|---------|-------|
| **I** | Independent | Can this be developed and shipped alone? |
| **N** | Negotiable | Can the details be discussed? (Not a spec.) |
| **V** | Valuable | Does it deliver value to the user or business? |
| **E** | Estimable | Can the team estimate effort? |
| **S** | Small | Can it be completed in one sprint? |
| **T** | Testable | Does it have clear acceptance criteria? |

> **Note:** "Small" doesn't mean trivial. A story that takes 3-5 days is fine. If it's 8+ points, split it.

## Acceptance Criteria

Acceptance criteria define the **boundaries** of a story — what "done" means from the user's perspective.

### Gherkin Format (Given / When / Then)

```gherkin
Feature: Password Reset
  As a logged-in user
  I want to reset my password
  So that I can regain access to my account

  Scenario: Successful password reset
    Given I am on the login page
    When I click "Forgot password"
    And I enter my email address
    And I submit the form
    Then I receive a password reset email
    And the email contains a reset link

  Scenario: Invalid email address
    Given I am on the login page
    When I enter a non-existent email address
    And I submit the form
    Then I see a message: "If that email exists, we've sent a reset link"
    And no email is sent
```

### Non-Gherkin Acceptance Criteria

```markdown
- [ ] Reset link expires after 1 hour
- [ ] User can only request reset once every 5 minutes
- [ ] Reset link is single-use
- [ ] New password meets strength requirements (8+ chars, mixed case, number)
- [ ] User is logged in automatically after successful reset
```

> **Tip:** Acceptance criteria are a **conversation aid**, not a legal contract. The team should discuss them at planning, not just read them.

## Epics

An **epic** is a large user story that can't fit in one sprint. It's a placeholder for a set of related stories.

```
EPIC: User Onboarding
  ├── As a new user, I want to sign up with email
  ├── As a new user, I want to verify my email address
  ├── As a new user, I want to create my profile
  ├── As a new user, I want to take a tour of the dashboard
  └── As a new user, I want to invite my teammates
```

## Story Splitting Techniques

| Technique | Example |
|-----------|---------|
| **By workflow steps** | "Checkout" → Add to cart → Enter address → Enter payment → Confirm |
| **By user role** | "Reporting" → Admin report → Manager report → Team report |
| **By happy vs edge cases** | "Password reset" → Successful reset → Invalid email → Expired link |
| **By platform** | "Mobile app" → iOS → Android → Web |
| **Spike first** | "Recommendation engine" → Research algorithms → Build MVP → Iterate |
| **Defer constraints** | "Payment" → Accept credit cards → Accept PayPal → Fraud detection |

**When a story is too big:** You can't estimate it confidently, it takes more than a sprint, or the acceptance criteria fill a page. Split it.

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Stories are specs | Every detail specified, no room for team creativity | Write goals, not instructions |
| No acceptance criteria | "Done" is ambiguous | Always include AC |
| Too large | Can't estimate, takes multiple sprints | Split until it fits one sprint |
| Technical stories | "Refactor the database layer" — what user value? | Express as the user benefit |
| No INVEST review | Stories fail silently | Check INVEST before planning |
| Writing stories for everyone | "As a user" is too vague | Be specific about the role |

## Better Alternatives to User Stories

| Technique | When | How |
|-----------|------|-----|
| **Job Stories** | When the user's context matters more than their identity | `When [situation], I want to [motivation], so I can [outcome]` |
| **Feature specs** | When the requirement is well-understood and low-risk | Traditional specification document |
| **Use cases** | When you need detailed interaction flows | Numbered steps with extensions |

### Job Story Example

```
When I'm traveling abroad,
I want to quickly check if my card will work,
So I can avoid embarrassing declined payments.
```

## Related Topics

- [Estimation & Planning](estimation-and-planning.md) — Stories are the unit of estimation
- [Scrum](scrum.md) — Stories live in the product backlog
- [Sprint Execution](sprint-execution.md) — How stories move through a sprint

## Further Learning

- *User Stories Applied* — Mike Cohn
- *Mapping User Stories in Agile* — Jeff Patton
- [INVEST checklist](https://xp123.com/articles/invest-in-good-stories-and-smart-tasks/)

---

> **Next:** [Estimation & Planning](estimation-and-planning.md) | **Previous:** [Kanban](kanban.md)
