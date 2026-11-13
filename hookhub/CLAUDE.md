# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

HookHub is a Next.js 15.4.6 application using the App Router architecture with TypeScript and Tailwind CSS.

## Essential Commands

```bash
# Development
npm run dev         # Start development server on http://localhost:3000

# Production
npm run build       # Create production build
npm run start       # Start production server

# Code Quality
npm run lint        # Run ESLint
```

## Architecture

- **Framework**: Next.js 15.4.6 with App Router
- **Structure**: All application code lives in `src/app/`
- **Styling**: Tailwind CSS 4.x (no custom config file - uses defaults)
- **TypeScript**: Configured with path aliases (`@/*` → `./src/*`)

## Key Files

- `src/app/layout.tsx` - Root layout with Geist font setup
- `src/app/page.tsx` - Home page component
- `src/app/globals.css` - Global styles and Tailwind directives

## Development Notes

- No test framework is currently set up
- Uses npm as package manager (package-lock.json present)
- ESLint configured with Next.js defaults
- Supports both light and dark modes via Tailwind

## Testing Strategy

- Use Playwright MCP for UI testing
- Save screenshots in `/memory/screenshots` directory

# Project standards for Claude agents

All Claude agents operating in this repo — locally and in CI — read this file
first. It defines the rules they apply and the formats they produce.

## Git conventions

- Base branch for all PRs: `develop`
- Compare diffs against `origin/develop` unless explicitly told otherwise
- Never commit or push from an agent run unless the task explicitly asks for it

## Code review standards

When reviewing a PR:

1. **Accuracy over completeness** — only report what you can verify from the
   diff and the code. If you cannot confirm a bug exists, say so.
2. **Cite locations** — every finding requires a `file:line` reference.
3. **No speculation** — if you can't confirm a bug, say "None found" rather
   than hedging with "could potentially".
4. **Respect scope** — review what changed in this PR, not the entire codebase.

## PR description format

All PR descriptions in this repo follow this template. Both the PR Writer agent
and human authors should use it:

```
## Summary
<2-4 sentences: what the change does and why>

## Changes
- <file or area>: <what changed>
- ...

## How to test
<concrete steps a reviewer can follow to verify the change works>

## Risks / notes
<known edge cases, follow-ups, gaps in test coverage, or things to watch>
```

**What "accurate" means for summaries:**

- Describe what the code actually does, not what you hope it does
- If tests are absent or thin, say so under Risks
- Do not claim "fixes all edge cases" unless the diff shows comprehensive coverage

## Custom skills used in review

If `.claude/skills/` contains any skill files relevant to the language or
framework in use (e.g. `python-security.md`, `typescript-patterns.md`), both
agents should read and apply those skills before writing their output.

## Comment tagging

When posting PR comments via `gh pr comment`, always begin the body with the
agent identifier tag so comments can be identified and idempotently replaced:

- PR Writer output begins with: `<!-- pr-writer -->`
- Adversarial Judge output begins with: `<!-- adversarial-judge -->`

## What agents must NOT do

- Commit or push code
- Approve or merge the PR
- Dismiss existing reviews
- Edit or delete comments left by other agents or humans
