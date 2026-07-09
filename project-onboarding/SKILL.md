---
name: project-onboarding
description: Repository onboarding workflow for agents before contributing code. Use when an agent is asked to familiarize itself with a project, understand an existing repository, identify implementation principles and conventions, map architecture, data flow, naming, caching, testing, build/deploy patterns, or prepare to work on future features with minimal mistakes.
---

# Project Onboarding

## Overview

Use this skill to understand an existing codebase before making changes. The goal is to build enough project-specific context to work within current conventions instead of writing against them.

## Ground Rules

- Do not write code during onboarding unless the user explicitly asks for fixes.
- Do not assume project conventions from language, framework, or prior experience; verify them from repository files.
- Ask the user questions wherever there is uncertainty, ambiguity, conflicting evidence, or a decision that cannot be safely inferred from the repo. This is compulsory.
- Do not make assumptions when facts are discoverable from local context. Inspect the repo instead.
- Preserve the user's worktree. Check status before editing in later tasks, and never revert changes you did not make.
- Prefer primary project sources: README files, docs, config files, package/build files, source code, tests, migrations, CI, and deployment config.
- Use fast local search tools such as `rg --files` and `rg` when available.

## Workflow

1. Establish repository shape.
   - Run `pwd`, list files, and inspect `git status --short`.
   - Identify major apps/packages, documentation, build files, test files, generated files, scripts, CI, deployment config, and environment examples.
   - Note whether the worktree is dirty and which areas appear modified.

2. Read project documentation first.
   - Read root README, app/package READMEs, architecture docs, style guides, product docs, implementation guides, and status docs.
   - Treat docs as hypotheses until verified against code.
   - Record mismatches between documentation and implementation.

3. Inspect runtime and tooling conventions.
   - Identify languages, frameworks, package managers, dependency files, lint/format/typecheck config, test commands, build commands, migration tools, and local run commands.
   - Do not install dependencies or call the network unless the user approves or the environment already allows it.

4. Map architecture and boundaries.
   - Find entry points, routing, service layers, domain modules, shared libraries, data models, schemas/types, middleware, auth, background jobs, and external integrations.
   - Identify which layer owns business logic, validation, persistence, side effects, and UI state.
   - Note import/export patterns and public module boundaries.

5. Understand data flow.
   - Trace representative reads and writes from UI/API/CLI entry point through services, storage, and back to response/rendering.
   - Identify request/response contracts, shared types, DTOs, schemas, serialization rules, and error shapes.
   - Identify pagination, filtering, sorting, search, upload, auth, and background processing patterns if present.

6. Understand caching and state.
   - Find client caches, server caches, persistence caches, invalidation rules, stale times, memoization, queues, background jobs, scheduled jobs, and idempotency patterns.
   - Identify where fresh data is required and where stale data is acceptable.

7. Learn naming and style conventions.
   - Inspect file naming, folder naming, function/class naming, route naming, database/table/column naming, event/job naming, and test naming.
   - Identify formatting conventions from config and existing files.
   - For UI projects, identify design tokens, component patterns, accessibility conventions, responsive patterns, and when hardcoded values are discouraged.

8. Inspect testing and validation.
   - Locate test suites, fixtures, factories, mocks, snapshots, contract tests, and scripts.
   - Identify the smallest meaningful validation command for future changes.
   - If no tests exist, note the gap and look for lint/type/build checks.

9. Identify risks and open questions.
   - List sharp edges, documented/implemented mismatches, TODOs that affect future work, fragile integrations, hidden assumptions, missing tests, and environment prerequisites.
   - Ask the user for clarification before proceeding when uncertainty could change implementation choices.

10. Summarize actionable conventions.
    - Keep the summary concise and practical.
    - Focus on rules that will prevent future mistakes: where to add code, which abstractions to use, how to fetch data, how to invalidate cache, how to name things, how to validate changes, and what not to touch.

## Optional Findings File

Do not create a file by default. Usually, keep the findings in conversation context and continue working from that context.

Create a file only when the user asks for persistent notes, multiple agents will use the findings, the onboarding result is large enough to be useful later, or the session context is likely to be lost.

Recommended filename: `AGENT_ONBOARDING_NOTES.md`.

If creating this file:
- Put it near the repository root unless the user requests another location.
- Keep it factual and repo-specific.
- Include date, scope inspected, conventions, validation commands, open questions, and known mismatches.
- Avoid duplicating full README content.
- Update it when future discoveries invalidate earlier notes.

## Report Format

When reporting onboarding findings, prefer this structure:

- Repository shape
- Core architecture
- Data flow and API boundaries
- Caching/state conventions
- Naming/style conventions
- Testing/validation commands
- Risks, mismatches, and open questions
- Practical rules for future contributions

Use file references for important files when the environment supports clickable paths.
