---
paths:
  - "src/pages/**/*.ts"
---

# Page Object Rules

- Every page object class must extend `BasePage` from `./base.page`
- Locators must be declared as `readonly Locator` properties on the class constructor
- Methods represent user actions (navigate, click, fill) — never assertions
- Never call `expect()` inside a page object method
- Constructor must call `super(page, config)` before setting locators
- Prefer `page.getByRole()`, `page.getByLabel()`, and `page.getByText()` over raw CSS selectors where possible
- Use `async/await` for all navigation and interaction methods
- Return type annotations are required on all public methods
- Do not use `any` type — use explicit types or `unknown` with a type guard
