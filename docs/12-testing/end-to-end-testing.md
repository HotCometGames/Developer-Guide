# End-to-End Testing

> Testing complete user workflows through the full application stack, from browser to backend.

> **Related:** [Integration Testing](integration-testing.md) | [JavaScript Testing](javascript-testing.md) | [CI/CD Pipelines](../13-deployment/ci-cd-pipelines.md)

---

## What Is It?

An end-to-end (E2E) test simulates a real user interacting with your application — clicking buttons, filling forms, navigating pages — and asserts the expected outcomes. It exercises the entire stack: frontend, backend, database, and external services.

## Playwright

Primary E2E tool for this handbook. Cross-browser, fast, reliable.

### Setup

```bash
npm init playwright@latest
npx playwright install
```

### Basic Test

```typescript
import { test, expect } from '@playwright/test';

test('user can complete purchase flow', async ({ page }) => {
  await page.goto('/products');
  await page.click('text=Add to Cart');
  await page.click('text=Checkout');
  await page.fill('#email', 'user@example.com');
  await page.fill('#card', '4242424242424242');
  await page.click('text=Pay');

  await expect(page.locator('.order-confirmation')).toBeVisible();
  await expect(page.locator('.order-number')).not.toBeEmpty();
});
```

### Key Features

| Feature | Usage |
|---------|-------|
| Locators | `page.getByRole()`, `page.getByText()`, `page.getByTestId()` |
| Auto-waiting | Built-in — no `sleep()` calls |
| Trace viewer | `--trace on` for debugging CI failures |
| Component testing | Test components in isolation |
| Mobile emulation | `playwright.devices['iPhone 13']` |
| API mocking | `page.route()` to intercept network requests |

## Cypress

Alternative to Playwright. Different architecture — runs in the browser.

```javascript
describe('Login flow', () => {
  it('shows error on invalid credentials', () => {
    cy.visit('/login');
    cy.get('#email').type('bad@email.com');
    cy.get('#password').type('wrong');
    cy.get('button').click();
    cy.contains('.error', 'Invalid credentials');
  });
});
```

## Visual Testing

Catches UI regressions by comparing screenshots:

```typescript
// Playwright + visual diff
test('homepage matches snapshot', async ({ page }) => {
  await page.goto('/');
  await expect(page).toHaveScreenshot('homepage.png');
});
```

| Tool | Integration | Storage |
|------|-------------|---------|
| Playwright built-in | Direct | Local file system |
| Percy | CI-friendly | Cloud |
| Chromatic | Storybook-focused | Cloud |

## CI Integration

```yaml
# .github/workflows/e2e.yml
jobs:
  e2e:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npm run dev & npx wait-on http://localhost:3000
      - run: npx playwright test
      - uses: actions/upload-artifact@v4
        if: failure()
        with:
          name: playwright-report
          path: playwright-report/
```

## Best Practices

- **Test critical paths only** — login, purchase, search — not every UI permutation
- **Use data-testid attributes** — `data-testid="submit-btn"` instead of fragile CSS selectors
- **Keep tests independent** — each test sets up its own state
- **Run against a real backend** — don't mock the API in E2E tests
- **Invest in traceability** — screenshots and videos on failure save hours

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Too many E2E tests | Slow, brittle suite | Follow test pyramid |
| Flaky selectors | Tests fail randomly | Prefer `getByRole`/`getByTestId` |
| No CI traces | Can't debug failures | Enable tracing on CI |
| Shared test state | Order-dependent failures | Isolate per-test data |
| Tests that sleep | Slow and fragile | Use auto-waiting or `waitFor` |

## What's Next?

E2E tests validate the full stack. For faster feedback, pair them with solid [Unit](unit-testing.md) and [Integration](integration-testing.md) tests following the test pyramid.
