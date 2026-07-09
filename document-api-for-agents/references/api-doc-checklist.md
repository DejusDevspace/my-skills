# API Documentation Checklist

## What To Inspect

- route declarations and router configuration
- request handlers, controllers, resolvers, or endpoint functions
- request validation rules, schemas, DTOs, or parser definitions
- response serializers, presenters, resources, transformers, or DTOs
- middleware, guards, policies, filters, interceptors, or hooks
- auth, permissions, rate limits, uploads, jobs, events, and integration code that changes API behavior
- config values and environment defaults that change API behavior
- tests or fixtures that clarify request/response contracts
- existing docs that are clearly current

## What To Extract

- route paths and methods
- public vs protected access
- permission or role checks
- query filters
- pagination conventions
- request validation rules
- response envelopes and resource shapes
- error responses and status codes
- special flows such as webhooks, OTP, batch upload, reissue, or lookup endpoints
- background side effects, async processing, events, and idempotency behavior that affect clients

## What To Write

- `openapi.yaml` as the canonical contract
- `README.md` as the agent-facing guide

## What To Avoid

- commented-out routes
- stale examples that no longer match code
- legacy request collections unless the user explicitly wants them updated
- invented endpoints, fields, or behaviors
- assumptions based on a framework or language instead of verified repository code
