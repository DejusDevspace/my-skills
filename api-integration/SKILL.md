---
name: api-integration
description: A robust methodology for integrating frontend applications with a backend API. Use when asked to integrate an API, standardizing API fetching, or connecting frontend pages to backend endpoints.
version: "1.0"
---

# API Integration Skill

**Name:** Standardized API Integration
**Description:** A robust methodology for integrating frontend applications with a backend API. This skill ensures that integrations are consistent, standardized, and correctly align with existing repository patterns or API documentation.

## Trigger
Use this skill when the user requests to:
- "Integrate a page to the API"
- "Connect the frontend to the backend"
- "Standardize API fetching"
- "Migrate mock data to live API data"

## Workflow Instructions

When tasked with integrating an API, follow this strict sequential workflow:

### 1. Analyze and Understand the Environment
Before writing any code, you must determine if this is a fresh integration or an addition to an existing system.

- **Check for Existing Conventions:** Search the repository for existing API configurations (e.g., `constants/index.ts`, `services/`, hooks like `useSWR` or `useQuery`).
  - *If existing integrations are found:* Thoroughly study them. Your new integration **must exactly replicate** the established conventions (e.g., how endpoints are constructed, how state/pagination is handled, how error banners are displayed, how data fetchers are configured).
  - *If it is a new repository (or no prior integration exists):* Locate the API documentation (e.g., `openapi.yaml`, Swagger docs, or Markdown files) in the repository. Use these specifications to establish a clean, standard integration architecture from scratch.

### 2. Standardize Endpoints & Types
- Define all API endpoint paths as central constants (e.g., in a `constants/index.ts` file) rather than hardcoding string paths directly into services or components.
- Validate that your planned endpoints and request/response shapes perfectly match the OpenAPI schema or API documentation.
- Define or update strict TypeScript interfaces/types for the API requests, responses, and UI models.

### 3. Handle Data Fetching & State
- **Listing/Read Operations:** Implement data fetching logic using the repository's preferred data fetching library (e.g., `useSWR`, `React Query`, or native `fetch` in Next.js App Router). Make sure to pass along any required query parameters natively (e.g., pagination `page`, `limit`, filters, and sorting).
- **Mutations (Create/Update/Delete):** Ensure that mutations hit the live API endpoints (replacing any mock logic like `setTimeout`).
- **Cache Invalidation:** After a successful mutation, ensure the frontend cache is invalidated/refreshed (e.g., calling `mutate()` in SWR) so the UI immediately reflects the new state without requiring a hard reload.

### 4. Require Clarification over Assumptions
- **Do NOT make assumptions.** If the existing conventions are contradictory (e.g., a service file handles state manually while another component uses a fetching hook), or if the frontend routes do not match the API documentation, STOP.
- Explicitly ask the user for clarification on which standard to adopt before writing any code.

## Verification
- Verify that there are no hardcoded string URLs remaining in the component or service files.
- Verify that loading, empty, and error states are accounted for.
- Verify that types match the schema specifications.
