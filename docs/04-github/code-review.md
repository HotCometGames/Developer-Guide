# Code Review

> Reviewing code on GitHub: giving and receiving feedback through Pull Requests.

> **Related:** [Pull Requests](pull-requests.md) | [GitHub CLI](github-cli.md)

---

## What Is It?

Code review is the practice of having other developers read and critique your code before it merges. GitHub's review system runs inside Pull Requests with line-level comments, approvals, and required checks.

## The Reviewer's Job

Your goal as a reviewer is not to catch every typo. It's to ensure the code is:

- **Correct** — does it solve the problem?
- **Maintainable** — will future developers understand it?
- **Secure** — does it introduce vulnerabilities?
- **Tested** — are there tests for the new behavior?
- **Consistent** — does it follow the project's style?

## Reviewing a PR

### Step-by-Step

1. Open the PR and read the description — understand the context
2. Go to **Files changed** tab
3. Scan the diff from top to bottom
4. Click the **+** on any line to leave a comment
5. At the top right, submit your review:
   - **Comment** — general notes, questions, or suggestions
   - **Approve** — the code is ready to merge
   - **Request changes** — blocking issues must be resolved first

### What to Look For

| Category | Questions to Ask |
|----------|-----------------|
| Logic | Does this handle edge cases? Are there off-by-one errors? |
| Naming | Do names reflect what the code does? |
| Structure | Is this function too long? Should it be split? |
| Testing | Are the tests meaningful? Do they cover failure modes? |
| Performance | Is this doing unnecessary work? Is there a simpler approach? |
| Security | Are user inputs validated? Are secrets exposed? |
| Style | Does it match the project's linter and formatting rules? |

## Suggesting Changes

GitHub supports suggestion blocks:

```
-let x = 10;
+const x = 10;
```

The author can accept the suggestion with one click.

```bash
gh pr review 42 --approve                              # approve
gh pr review 42 --comment "Looks good, one nit"         # comment
gh pr review 42 --request-changes "Fix the edge case"   # request changes
```

## The Author's Job

### Before Requesting Review

- **Self-review** — diff your own code first. Catch what you can
- **Write a good description** — explain what changed and why
- **Keep it small** — PRs under 300 lines get better reviews
- **Run tests locally** — don't waste reviewers' time on failures

### Responding to Feedback

- **Be grateful** — reviewers are helping you
- **Push fix commits** — don't force-push; let reviewers see what changed between review rounds
- **Resolve conversations** — mark resolved when addressed
- **Explain when you disagree** — "I considered that but chose X because Y"
- **Don't take it personally** — review is about the code, not you

## Review Depth Levels

| Level | What You Do | Time |
|-------|-------------|------|
| **Light** | Quick scan for obvious bugs, style, and security | 5-10 min |
| **Standard** | Read all diffs, check logic, run locally if needed | 15-30 min |
| **Deep** | Verify every branch, test coverage, check for regressions | 30-60 min |

Adjust depth based on risk. A UI text change gets light review; a payment processing change gets deep review.

## Automated Review

### Required Checks

Branch protection rules can require:

- At least one approved review
- All conversations resolved
- CI checks passing (tests, lint, build)
- Up-to-date branch (must be based on latest main)

### CODEOWNERS

In `.github/CODEOWNERS`, auto-assign reviewers based on file paths:

```
# Global owners
* @team-leads

# Frontend code
/src/ui/   @frontend-team

# Backend code
/src/api/  @backend-team
```

## Best Practices

- **Review the approach, not just the code** — ask "should we solve it this way?" not just "is this line right?"
- **Be specific** — instead of "this is wrong", say "this comparison will fail when `count` is 0"
- **Praise good code** — "this error handling is clever" goes a long way
- **Use emoji reactions** — thumbs up, rocket ship, heart — quick positive signals
- **Don't bikeshed** — avoid blocking the PR over style preferences
- **Review in short sessions** — review quality drops after 30 minutes
