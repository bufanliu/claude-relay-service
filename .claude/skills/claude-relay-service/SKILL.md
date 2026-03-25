```markdown
# claude-relay-service Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute effectively to the `claude-relay-service` codebase, a JavaScript/Express service for relaying requests to Claude and related AI models. You'll learn the project's coding conventions, how to implement and test common workflows (like updating model pricing or API key permissions), and the commands used to streamline frequent tasks.

---

## Coding Conventions

**File Naming**
- Use `camelCase` for JavaScript files.
  - Example: `pricingService.js`, `bedrockRelayService.js`

**Import Style**
- Use relative imports for modules.
  - Example:
    ```js
    const { calculatePrice } = require('../utils/pricingHelper');
    ```

**Export Style**
- Use named exports.
  - Example:
    ```js
    // pricingService.js
    function calculatePrice(model, tokens) { ... }
    module.exports = { calculatePrice };
    ```

**Commit Patterns**
- Prefix commits with `fix`, `chore`, `feat`, or `style`.
- Keep commit messages concise (~54 characters on average).
  - Example: `feat: add allow1mContext to API key model`

---

## Workflows

### Model Pricing or Pricing Logic Update
**Trigger:** When model pricing or context window changes, or new models are added that require pricing logic updates.  
**Command:** `/update-model-pricing`

1. Edit `resources/model-pricing/model_prices_and_context_window.json` to update or add pricing/context window info.
2. Update `src/services/pricingService.js` to adjust pricing calculation logic.
3. Update or add tests in `tests/pricingService.test.js` to verify new pricing logic.

**Example:**
```json
// model_prices_and_context_window.json
{
  "claude-v2": {
    "price_per_1k_tokens": 0.008,
    "context_window": 100000
  }
}
```
```js
// pricingService.js
function calculatePrice(model, tokens) {
  // Updated logic based on new pricing
}
module.exports = { calculatePrice };
```

---

### API Key Feature or Permission Update
**Trigger:** When a new API key feature/permission is needed (e.g., `allow1mContext`), or existing logic needs to be changed.  
**Command:** `/update-api-key-feature`

1. Update `src/models/redis.js` to add new API key fields.
2. Update `src/services/apiKeyService.js` to handle new fields in creation, validation, and update logic.
3. Update `src/middleware/auth.js` to attach new fields to request context.
4. Update `src/routes/admin/apiKeys.js` and `src/routes/api.js` for API changes.
5. Update admin UI in `web/admin-spa/src/components/apikeys/*Modal.vue` (Create, Edit, Batch Edit).

**Example:**
```js
// redis.js
const apiKeySchema = {
  key: String,
  allow1mContext: Boolean, // new field
  ...
};
```
```vue
<!-- CreateApiKeyModal.vue -->
<template>
  <input v-model="apiKey.allow1mContext" type="checkbox" />
</template>
```

---

### Bedrock Relay Auth or Forwarding Fix
**Trigger:** When Bedrock relay integration requires authentication fixes, token support, or new parameter passthrough.  
**Command:** `/fix-bedrock-relay-auth`

1. Edit `src/services/relay/bedrockRelayService.js` to fix auth/token logic or parameter handling.
2. Optionally update `src/routes/api.js` if API-level logic is affected.

**Example:**
```js
// bedrockRelayService.js
function forwardRequest(req, res) {
  const token = req.headers['authorization'];
  // Fix token forwarding logic
}
```

---

### Account or Routing Policy Enhancement
**Trigger:** When account routing, temporary block, or cooldown/backoff logic needs to be improved or made configurable.  
**Command:** `/enhance-account-routing`

1. Edit `src/services/account/claudeAccountService.js` and `src/services/relay/claudeRelayService.js` for logic changes.
2. Update `src/services/scheduler/unifiedClaudeScheduler.js` and `src/utils/upstreamErrorHelper.js` for policy/backoff.
3. Update `src/utils/tempUnavailablePolicy.js` for policy extraction.
4. Update admin UI: `web/admin-spa/src/components/accounts/AccountForm.vue`, `TempUnavailablePolicyFields.vue`, `AccountsView.vue`.
5. Update config/docs: `config/config.example.js`, `.env.example`, `README.md`, `README_EN.md`.

**Example:**
```js
// tempUnavailablePolicy.js
function shouldBlockAccount(account) {
  // Enhanced logic for temporary unavailability
}
```
```vue
<!-- TempUnavailablePolicyFields.vue -->
<template>
  <input v-model="policy.cooldownSeconds" type="number" />
</template>
```

---

### Version Bump Release Sync
**Trigger:** When a new release is cut and the VERSION file needs to be updated.  
**Command:** `/bump-version`

1. Update `VERSION` file with the new release number.

**Example:**
```
# VERSION
1.4.2
```

---

## Testing Patterns

- **Framework:** [Jest](https://jestjs.io/)
- **Test File Pattern:** Files end with `.test.js`
  - Example: `pricingService.test.js`
- **Test Example:**
    ```js
    // pricingService.test.js
    const { calculatePrice } = require('../src/services/pricingService');

    test('calculates price for claude-v2', () => {
      expect(calculatePrice('claude-v2', 1000)).toBe(0.008);
    });
    ```

---

## Commands

| Command                  | Purpose                                                        |
|--------------------------|----------------------------------------------------------------|
| /update-model-pricing    | Update model pricing, context window, or pricing logic         |
| /update-api-key-feature  | Add or modify API key features or permissions                  |
| /fix-bedrock-relay-auth  | Fix or enhance Bedrock relay authentication/forwarding         |
| /enhance-account-routing | Enhance account routing, blocking, or temp-unavailable policy  |
| /bump-version            | Synchronize the VERSION file for a new release                 |
```
