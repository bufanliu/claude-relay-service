---
name: model-pricing-or-pricing-logic-update
description: Workflow command scaffold for model-pricing-or-pricing-logic-update in claude-relay-service.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /model-pricing-or-pricing-logic-update

Use this workflow when working on **model-pricing-or-pricing-logic-update** in `claude-relay-service`.

## Goal

Update model pricing, context window, or pricing logic for models (often for new models or changes in provider pricing).

## Common Files

- `resources/model-pricing/model_prices_and_context_window.json`
- `src/services/pricingService.js`
- `tests/pricingService.test.js`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit resources/model-pricing/model_prices_and_context_window.json to update or add pricing/context window info.
- Update src/services/pricingService.js to adjust pricing calculation logic.
- Update or add tests in tests/pricingService.test.js to verify new pricing logic.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.