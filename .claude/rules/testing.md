---
paths:
  - "tests/**/*.spec.ts"
  - "tests/**/*.test.ts"
---

# Test File Rules

- Import `test` and `expect` from `@fixtures/site.fixture`, never directly from `@playwright/test`
- Every `test()` call must include at least one tag: `@smoke`, `@navigation`, `@forms`, `@functional`, `@visual`, `@responsive`, or `@custom`
- Never hardcode the site URL — use `siteConfig.url` from the fixture
- Never submit forms — test field interactions and validation only
- Never call `page.waitForTimeout()` — use `waitForSelector`, `toBeVisible`, or Playwright auto-waiting
- Keep tests independent — each test must be able to run in isolation
- Put the `@tag` at the end of the test name string, not in a separate annotation
- Describe blocks should name the page or feature area, not the file name
