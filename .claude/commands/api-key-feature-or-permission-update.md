---
name: api-key-feature-or-permission-update
description: Workflow command scaffold for api-key-feature-or-permission-update in claude-relay-service.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /api-key-feature-or-permission-update

Use this workflow when working on **api-key-feature-or-permission-update** in `claude-relay-service`.

## Goal

Add or modify API key features or permissions, including new fields, validation, and admin UI for API keys.

## Common Files

- `src/models/redis.js`
- `src/services/apiKeyService.js`
- `src/middleware/auth.js`
- `src/routes/admin/apiKeys.js`
- `src/routes/api.js`
- `web/admin-spa/src/components/apikeys/BatchEditApiKeyModal.vue`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update src/models/redis.js to add new API key fields.
- Update src/services/apiKeyService.js to handle new fields in creation, validation, and update logic.
- Update src/middleware/auth.js to attach new fields to request context.
- Update src/routes/admin/apiKeys.js and src/routes/api.js for API changes.
- Update web/admin-spa/src/components/apikeys/*Modal.vue for admin UI (Create, Edit, Batch Edit).

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.