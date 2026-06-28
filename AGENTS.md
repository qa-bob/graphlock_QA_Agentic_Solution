# AGENTS.md — Sub-Agent Documentation

> This file documents every Claude Code sub-agent defined in this repository.
> Claude Code reads `CLAUDE.md` natively; if another coding agent reads `AGENTS.md`, the project `CLAUDE.md` imports this file via `@AGENTS.md`.

Sub-agents are specialized AI workers defined in `.claude/agents/`. Each runs in its own context window with a focused system prompt, specific tool access, and independent permissions. Claude delegates to them automatically when the task matches the agent's description, or you can invoke one explicitly.

---

## Agent: `site-analyzer`

**File:** `.claude/agents/site-analyzer.md`
**Model:** Sonnet (default)
**Tools:** `WebFetch`, `Read`, `Write`, `Bash`

### Purpose

Crawls a live website and produces a fully-populated `site.config.json`. Used when onboarding a new site or verifying the config is still accurate after a redesign.

### When Claude invokes it

- You run `/analyze-site`
- You ask Claude to "analyze the site" or "update site.config.json"
- You onboard this framework to a new company URL

### What it does

1. Resolves the canonical URL (follows all redirects)
2. Navigates with `waitUntil: 'networkidle'`; waits extra for SPA hydration
3. Dismisses cookie consent banners
4. Extracts all nav links (text + href)
5. Detects contact forms across current page + `/contact`, `/contact-us`
6. Infers the industry from heading and paragraph copy
7. Detects auth gating (redirect to `login`/`signin`/`auth` URL)
8. Outputs a valid `site.config.json` + issues checklist + confidence rating

### Output

- Updated `site.config.json`
- Checklist of SEO/accessibility issues found
- Confidence level: High / Medium / Low with reasoning

---

## Agent: `test-generator`

**File:** `.claude/agents/test-generator.md`
**Model:** Sonnet (default)
**Tools:** `Read`, `Write`, `Edit`, `Bash`, `WebFetch`

### Purpose

Reads `site.config.json` and the live site to generate site-specific Playwright test files beyond the shared generic suites. Output lands in `tests/custom/`.

### When Claude invokes it

- You run `/generate-full-suite`
- You ask Claude to "generate tests for the pricing page" or similar
- You want tests for a recently discovered bug

### What it does

1. Reads `site.config.json`
2. Identifies coverage gaps in existing suites
3. Plans test scenarios before writing any code
4. Adds locators to page objects in `src/pages/`
5. Writes spec files to `tests/custom/<scenario>.spec.ts`
6. Tags all tests with `@custom` plus appropriate suite tags

### Conventions for generated files

- File: `tests/custom/<kebab-case-description>.spec.ts`
- Imports from `@fixtures/site.fixture`
- One `describe` block per page or feature area
- JSDoc comment at the top explaining what is tested and why it is site-specific
- Strict TypeScript — no implicit `any`

---

## Adding a New Sub-Agent

1. Create `.claude/agents/<name>.md`
2. Add YAML frontmatter with at minimum `name` and `description`:

```yaml
---
name: my-agent
description: One sentence explaining when Claude should delegate here. Be specific — Claude uses this to decide.
tools: Read, Write, Bash
model: sonnet
---

You are a specialized agent for...
```

3. Write the system prompt body in Markdown below the frontmatter
4. Document the agent in this file

Sub-agents are loaded at session start. Restart the session after adding a new file, or use `/agents` to manage them interactively.

---

## Related

- [Skills.md](./Skills.md) — Slash commands and skill documentation
- [CLAUDE.md](./CLAUDE.md) — Project-level instructions for Claude Code
- `.claude/agents/` — Agent definition files
