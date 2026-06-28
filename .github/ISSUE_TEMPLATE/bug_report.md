---
name: Bug Report — Failing Test
about: A test is failing unexpectedly or producing incorrect results
title: "[BUG] <test name> fails on <suite>"
labels: bug, test-failure
assignees: ''
---

## Test Details

- **Test name:** <!-- e.g., "all nav links are reachable @navigation" -->
- **File:** <!-- e.g., tests/navigation/nav-links.spec.ts -->
- **Suite tag:** <!-- @smoke / @navigation / @forms / @functional / @visual / @responsive -->
- **Project/browser:** <!-- chromium-desktop / mobile-chrome / tablet -->

## Expected Behavior

<!-- What should the test do? -->

## Actual Behavior

<!-- What actually happens? Paste the error message. -->

```
<error message here>
```

## Reproduction Steps

1. Run `npm run test:<suite>`
2. See failure for `<test name>`

## Environment

- **OS:**
- **Node.js version:** (`node --version`)
- **Playwright version:** (`npx playwright --version`)
- **Site URL:** https://graphlock.com
- **Site reachable at time of failure?** Yes / No

## Screenshots / Artifacts

<!-- Attach Playwright trace files, screenshots, or the HTML report if available. -->

## Likely Cause (if known)

<!-- Is this a selector change on the live site? A timing issue? A framework bug? -->
