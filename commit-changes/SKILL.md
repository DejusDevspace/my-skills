---
name: commit-changes
description: >-
  Creates well-structured commits from a batch of file changes. Groups files by
  layer (schema, service, router, etc.) and by side (frontend/backend).
  Generates an executable commit script with conventional commit messages. USE
  FOR: finalizing work, creating commits, preparing PRs, organizing changes into
  logical commits. DO NOT USE FOR: work that hasn't been written yet, mid-work
  snapshots, or exploratory branches where structure doesn't matter.
---

# Commit Changes Skill

Use this skill when you have a batch of finished changes and need to commit them
in a structured, reviewable way. The skill applies a consistent set of rules for
grouping, message style, and script generation regardless of the project or
language.

## Core Rules

### 1. Frontend/Backend Boundary - Always Separate

Frontend and backend changes **never** go in the same commit, even if they form
a single feature end-to-end. Each side gets its own commit (or set of commits).

### 2. Layer Grouping Within Each Side

Within each side, the AI groups files by layer based on **semantic coupling** -
files that depend on each other conceptually belong in the same commit.

| Typical layers (backend)       | Typical layers (frontend)     |
|--------------------------------|-------------------------------|
| Schema / DTO / Model           | Type / Interface              |
| Service / Logic                | API function                  |
| Router / Controller / Handler  | Hook / Query / Mutation       |
| Migration / DB                 | Page / Component              |

Patterns like `schema -> service -> router` or `types -> api -> hook -> component`
are natural groupings. The AI examines file dependencies and groups accordingly;
it explains the grouping in the commit script's comment block.

### 3. Single-Commit Exception

A single commit is appropriate only when **all changed files form one
indivisible modular change** - for example, renaming a function across the stack
(definition + imports + usages, all frontend or all backend).

### 4. No Churn Commits

Do not create a commit for a single file change that makes no sense on its own
(e.g., just a type definition without its consumers). Each commit should be
**logically complete and independently reviewable** within its layer.

## Commit Message Format

```text
<type>(<scope>): <short imperative summary, no period>

<optional body - one or more paragraphs explaining what and why, wrapped at 72
characters. Omit when the summary alone is sufficient.>
```

- **type**: `feat`, `fix`, `chore`, `refactor`, `test`, `docs`, `perf`, `style`
- **scope**: a short label for the layer or area (e.g. `schema`, `service`,
  `router`, `api`, `ui`, `types`, `hooks`)
- **imperative mood**: "add", "fix", "move", "rename", "extract", "replace"
- **no title period**: titles never end with a full stop
- **body optional**: use when context or rationale is non-obvious; omit when
  the title is self-explanatory

## Output

Generate an executable commit script (`commit_<descriptive_name>.sh`):

```bash
#!/usr/bin/env bash
set -euo pipefail

# ============================================================
# 1. <layer>: <one-line description>
# ============================================================
# <Explanation: why these files are grouped together>
git add <file1> <file2>
git commit -m "<type>(<scope>): <summary>

<body if needed>
"

# ============================================================
# 2. <layer>: <one-line description>
# ============================================================
...

git add <file3>
git commit -m "..."
```

The script must be idempotent-friendly: staged files that are already committed
are simply re-staged without harm.

## Before You Begin

1. **Read the diff / status** - understand what changed and which files depend
   on each other.
2. **Identify the sides** - classify each file as backend or frontend (if the
   project has both).
3. **Group by coupling** - cluster files within each side by conceptual
   dependency.
4. **Draft commit messages** - one per group, following the format above.
5. **Write the script** - with numbered sections, a brief explanation comment
   per group, and the git commands.
6. **Present** - show the script path and a summary of the commits to the user
   before they run it.
