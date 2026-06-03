# API Documentation Checklist

## What To Inspect

- `routes/*.php`
- controllers
- form requests
- resources
- middleware
- config values that change API behavior
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

## What To Write

- `openapi.yaml` as the canonical contract
- `README.md` as the agent-facing guide

## What To Avoid

- commented-out routes
- stale examples that no longer match code
- legacy request collections unless the user explicitly wants them updated
- invented endpoints, fields, or behaviors

