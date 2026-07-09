---
name: document-api-for-agents
description: Use when a user wants to inspect a repository's live API surface and produce agent-facing documentation such as OpenAPI and a concise Markdown guide from routes, handlers/controllers, request schemas, response serializers, middleware, and configuration. Use this when documenting APIs for frontend or agent integration, and keep legacy collections like Bruno untouched unless explicitly requested.
---

# Document API For Agents

## Overview

Use this skill to turn a backend repo into canonical API docs for an AI agent or frontend developer. The default output is a machine-readable OpenAPI spec plus a short Markdown usage guide.

## Workflow

1. Inspect the live API surface first.
   - Read route declarations, handlers/controllers, request validators or schemas, response serializers or presenters, middleware, config, and any existing docs that reflect current behavior.
   - Prefer `rg` and direct file reads.
2. Document only live behavior.
   - Include active routes, auth rules, permissions, filters, pagination, multipart uploads, webhooks, bulk operations, and error shapes that the code actually returns.
   - Exclude commented-out, deprecated, or inactive routes unless the user explicitly wants them.
3. Treat code as the source of truth.
   - Trust current handlers/controllers, request schemas, and response serializers over stale examples or old docs.
   - Resolve mismatches by matching implementation, not assumptions.
4. Write the docs in two layers.
   - `openapi.yaml` is the canonical machine-readable contract.
   - `README.md` is the human-readable integration guide for the agent and frontend.
5. Preserve legacy collections.
   - Do not update Bruno collections or similar sample request sets unless the user explicitly asks.
   - Mention them only as optional examples if they are still useful.

## Documentation Rules

- Prefer OpenAPI 3.1 YAML as the source of truth.
- Document method, path, auth, path params, query params, request bodies, response shapes, and status codes.
- Capture endpoint-specific conventions such as:
  - public vs protected access
  - role or permission gates
  - list filters and pagination parameters
  - multipart upload field names
  - nested payloads and alternate create paths
  - resource wrapper vs raw JSON responses
- Document only what the code supports now.
- If the target docs location is unclear, ask before writing.

## Output Shape

Default output package:

- `docs/api/openapi.yaml`
- `docs/api/README.md`

Use a different path only if the repository already has a clear documentation convention.

## Quality Check

- Verify YAML parses cleanly.
- Cross-check `$ref` targets and endpoint coverage.
- Confirm the docs answer the integration questions an AI agent would ask:
  - How do I authenticate?
  - Which endpoints are public?
  - What filters and payloads does each endpoint accept?
  - What shape does each endpoint return?
  - What permission gates or ownership rules apply?
