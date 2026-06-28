# Skills.md — Slash Commands and Skills Documentation

> This file documents every skill and slash command defined in this repository.
> Skills live in `.claude/commands/` (legacy, still fully supported) or `.claude/skills/<name>/SKILL.md` (new format).
> Both are invoked the same way: type `/skill-name` in a Claude Code session.

---

## Available Skills / Commands

### `/analyze-site`

**File:** `.claude/commands/analyze-site.md`
**Invoke:** `/analyze-site [url]`

Crawls the target website and produces a fully-populated `site.config.json`. If no URL is provided, reads the URL from the existing `site.config.json`.

**Steps:**
1. Navigate to the site with `waitUntil: 'networkidle'`
2. Extract page title, meta description, nav links, forms, H1, CTAs
3. Attempt `/contact`, `/contact-us` for contact form detection
4. Assess responsiveness at 390px viewport
5. Output updated `site.config.json` + issues checklist

**Use when:** onboarding a new site, verifying config after a redesign, or before writing new tests.

---

### `/generate-full-suite`

**File:** `.claude/commands/generate-full-suite.md`
**Invoke:** `/generate-full-suite`

Runs `/analyze-site` first, then generates the complete POM + test suites for every discovered page and feature. This is the "full onboarding" command for a brand-new site.

**Steps:**
1. Run `/analyze-site` to populate `site.config.json`
2. Discover all pages reachable from nav links
3. Create or update page object classes in `src/pages/`
4. Generate `tests/smoke/`, `tests/navigation/`, `tests/forms/`, `tests/functional/`, `tests/visual/`, `tests/responsive/`
5. Generate site-specific tests in `tests/custom/`
6. Run `npx tsc --noEmit` to verify TypeScript
7. Report what was created

**Use when:** setting up tests from scratch or after a major site redesign.

---

### `/run-smoke`

**File:** `.claude/commands/run-smoke.md`
**Invoke:** `/run-smoke`

Runs `npm run test:smoke` and displays a formatted pass/fail table with error details and suggested fixes for any failures.

**Output format:**
```
Site: GraphLock (https://graphlock.com)
Run: 2026-06-27 09:15:00   Duration: 8.2s

+--------------------------------------------------+--------+----------+
| Test                                             | Status | Duration |
+--------------------------------------------------+--------+----------+
| site homepage loads successfully                 | PASS   | 1.1s     |
| page loads within acceptable time               | PASS   | 2.9s     |
| ...                                              |        |          |
+--------------------------------------------------+--------+----------+
Total: 5   Passed: 5   Failed: 0   Warnings: 0
```

**Use when:** quick health check, pre-PR verification, or after a site deployment.

---

### `/update-baseline`

**File:** `.claude/commands/update-baseline.md`
**Invoke:** `/update-baseline`

Runs `npm run baseline` to refresh all visual regression snapshot files and reports what changed.

**Use when:** intentional UI changes have been deployed and the visual snapshots need to reflect the new design.

**Important:** Always review the diff before committing updated baselines. Only update when the change is expected.

---

### `/generate-report`

**File:** `.claude/commands/generate-report.md`
**Invoke:** `/generate-report`

Parses the latest Playwright test results and generates a formatted summary report showing pass rates, flaky tests, slowest tests, and coverage by suite tag.

**Use when:** reviewing results after a CI run or sharing a test status update.

---

## Adding a New Skill

### New format (recommended): `.claude/skills/<name>/SKILL.md`

```
.claude/skills/
└── my-skill/
    ├── SKILL.md          # Required — main instructions
    └── examples/         # Optional supporting files
```

`SKILL.md` frontmatter:

```yaml
---
description: One sentence explaining when Claude should load this skill automatically. Be specific.
---

## Instructions

Step-by-step instructions Claude follows when this skill runs...
```

### Legacy format (still supported): `.claude/commands/<name>.md`

```markdown
# /my-command

What this command does.

## Usage
/my-command [args]

## Steps
1. ...
2. ...
```

Both formats create a `/my-command` slash command. Skills take precedence over commands if names conflict.

---

## Dynamic Context Injection

Skills can inject live shell output into their instructions using `` !`command` `` syntax:

```yaml
---
description: Summarize current git diff
---

## Current diff

!`git diff HEAD`

## Instructions

Summarize the changes above...
```

Claude Code runs the command and replaces the line with its output before Claude sees the skill.

---

## Related

- [AGENTS.md](./AGENTS.md) — Sub-agent documentation
- [CLAUDE.md](./CLAUDE.md) — Project-level instructions
- `.claude/commands/` — Legacy command files
