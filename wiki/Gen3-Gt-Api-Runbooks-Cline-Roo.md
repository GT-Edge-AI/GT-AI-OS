## Start Here

Configure Cline or Roo Code extension OpenAI-compatible provider settings with GT API base URL, bearer key, and a published coding alias. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Cline / Roo Code** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://docs.cline.bot/customization/custom-model
- https://docs.roocode.com/getting-started/connecting-api-providers
- https://docs.cline.bot/features/auto-approve

### Configuration fields

- **Cline → openaiBaseUrl / OpenAI Base URL:** `https://<tenant-host>/api/tenant`
- **Cline → openaiApiKey:** `gtak_...`
- **Roo Code → openAiBaseUrl (OpenAI Compatible provider):** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Extension model field set to published alias |
| `POST /v1/chat/completions` | native | Extension OpenAI-compatible client → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Not used in standard Cline/Roo coding chat setup |
| `POST /v1/audio/transcriptions` | not_supported | Not supported in extension OpenAI path |
| `POST /v1/audio/speech` | not_supported | Not supported in extension OpenAI path |
| `POST /v1/images/generations` | not_supported | Not supported in extension OpenAI path |
| `POST /v1/conversations/files` | not_supported | Not applicable unless custom HTTP added |
| `POST /v1/datasets/{id}/files` | not_supported | Not applicable unless custom HTTP added |
| `GET /v1/files/{id}` | not_supported | Not applicable unless custom HTTP added |

### Not supported in this product

- Extension file contexts are local/editor-scoped — not GT conversation or dataset upload routes.

### Prerequisites

- Publish coding-focused agent aliases.
- Create dedicated inference key per rollout or developer.

### Setup steps

1. Open extension settings → set OpenAI-compatible Base URL to `https://<tenant-host>/api/tenant`.
2. Paste GT API bearer key into extension API key field.
3. Choose published alias as model id.
4. Validate one completion before enabling autonomous edit modes.

### GT extensions and caveats

- GT upload/conversation routes only if you add custom HTTP orchestration — not default extension behavior.
- Keep keys scoped tightly due to automated edit bursts.

### Validation checklist

- Extension connects and completes one task.
- Only intended aliases visible or selectable.
- Key revocation does not break unrelated integrations.

### Plain-text export

```text
Cline / Roo Code runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Configure Cline or Roo Code extension OpenAI-compatible provider settings with GT API base URL, bearer key, and a published coding alias.

Official documentation:
- https://docs.cline.bot/customization/custom-model
- https://docs.roocode.com/getting-started/connecting-api-providers
- https://docs.cline.bot/features/auto-approve

Configuration fields:
- Cline → openaiBaseUrl / OpenAI Base URL: https://<tenant-host>/api/tenant
- Cline → openaiApiKey: gtak_...
- Roo Code → openAiBaseUrl (OpenAI Compatible provider): https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): Extension model field set to published alias
- POST /v1/chat/completions (native): Extension OpenAI-compatible client → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Not used in standard Cline/Roo coding chat setup
- POST /v1/audio/transcriptions (not_supported): Not supported in extension OpenAI path
- POST /v1/audio/speech (not_supported): Not supported in extension OpenAI path
- POST /v1/images/generations (not_supported): Not supported in extension OpenAI path
- POST /v1/conversations/files (not_supported): Not applicable unless custom HTTP added
- POST /v1/datasets/{id}/files (not_supported): Not applicable unless custom HTTP added
- GET /v1/files/{id} (not_supported): Not applicable unless custom HTTP added

Not supported in this product:
- Extension file contexts are local/editor-scoped — not GT conversation or dataset upload routes.

Prerequisites:
- Publish coding-focused agent aliases.
- Create dedicated inference key per rollout or developer.

Setup steps:
1. Open extension settings → set OpenAI-compatible Base URL to `https://<tenant-host>/api/tenant`.
2. Paste GT API bearer key into extension API key field.
3. Choose published alias as model id.
4. Validate one completion before enabling autonomous edit modes.

GT extensions and caveats:
- GT upload/conversation routes only if you add custom HTTP orchestration — not default extension behavior.
- Keep keys scoped tightly due to automated edit bursts.

Validation checklist:
- Extension connects and completes one task.
- Only intended aliases visible or selectable.
- Key revocation does not break unrelated integrations.
```
