## Summary

<!-- What does this PR do? One paragraph max. -->

## Type of Change

- [ ] New test(s) added
- [ ] Existing test(s) updated
- [ ] New page object(s) added or updated
- [ ] Bug fix (broken test corrected)
- [ ] Visual baseline updated
- [ ] Config change (`site.config.json`, `playwright.config.ts`)
- [ ] Agent / skill / command update
- [ ] CI / tooling change
- [ ] Documentation only

## Test Coverage

<!-- Which test suites are affected? Check all that apply. -->

- [ ] `@smoke`
- [ ] `@navigation`
- [ ] `@forms`
- [ ] `@functional`
- [ ] `@visual`
- [ ] `@responsive`
- [ ] `@custom`

## Checklist

- [ ] `npm run typecheck` passes (zero TypeScript errors)
- [ ] `npm run lint` passes (zero ESLint errors)
- [ ] `npm run test:smoke` passes locally
- [ ] All new tests follow the POM conventions (no `expect()` in page objects)
- [ ] No hardcoded URLs in test files (uses `siteConfig.url`)
- [ ] No form submissions in tests
- [ ] Visual baseline changes are intentional and screenshots have been reviewed

## Visual Changes

<!-- If you updated visual baselines, paste before/after screenshots here. -->

## Notes for Reviewer

<!-- Anything the reviewer should know: flaky tests, external dependencies, known issues. -->
