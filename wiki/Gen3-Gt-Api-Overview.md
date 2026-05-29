## Start Here

Use the tenant GT API base URL (`https://<tenant-host>/api/tenant`) with a scoped bearer key. Validate `GET /v1/models` before enabling chat, embeddings, uploads, or GT conversation headers.

## Why this matters

External tools only see published inference and upload aliases. GT API keeps internal agent and dataset identifiers private while exposing OpenAI-shaped routes for compatible clients.

## Details

Open the **GT API** workspace (`/gt-api`) for **API Keys** and **Published Endpoints**. Full compatibility matrix, per-client runbooks, and API reference live in this Instructions section.

### Quickstart bundle

```text
Base URL: https://<tenant-host>/api/tenant
Authorization: Bearer gtak_...

List published models:
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  "https://<tenant-host>/api/tenant/v1/models"

Chat completion:
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/chat/completions" \
  -d '{
    "model": "agent-alias",
    "messages": [
      { "role": "user", "content": "Summarize the attached mission brief." }
    ]
  }'
```

### Getting started notices

### Simple inference-only rollout

Use this path when an integration only needs OpenAI-compatible model discovery and chat completion.

- Publish inference targets in `Published Endpoints`: agent aliases for configured agents, and published raw-model catalog entries when callers should use those names in `model` instead of an agent alias.
- Create an inference key limited to the exact agent aliases and raw-model targets (and inference scopes) that caller should reach; add prompt guardrail modules or extra prompt text on the key when policy requires it.
- Hand the caller only the bearer key and the `/api/tenant/v1/*` base URL.

### Advanced conversation plus uploads

Use this path when the client app needs one conversation-facing credential that can both chat and attach files.

- Create reusable inference and upload keys first so their allowlists stay independently auditable.
- Create the conversation-facing key from `API Keys`, linking it to those reusable runtime keys.
- Publish only the inference names the caller should see after authentication—agent aliases, raw-model catalog names, or both—then create a GT conversation explicitly before sending follow-up chat turns and file flows with `X-GT-Conversation-Id`.

### Custom OpenAI-compatible inference URL

Use this path when a third-party product is not listed in the matrix but lets you configure a custom OpenAI-compatible base URL and bearer key.

- Point the client at the tenant GT API base ending in `/api/tenant`, then validate `GET /v1/models` before enabling higher-level features.
- Start with a narrow inference key and at least one published inference name (agent alias or raw-model catalog entry), then add embeddings, uploads, or GT conversations only if the product truly needs them.
- If the product only supports vendor-native APIs and cannot target an arbitrary OpenAI-compatible URL, GT API is not a direct fit without a proxy layer.
