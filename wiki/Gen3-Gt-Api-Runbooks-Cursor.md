## Start Here

When the Cursor environment allows overriding the OpenAI API base URL, point it at GT API with a dedicated editor inference key and published coding alias. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Cursor** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://docs.cursor.com/settings/models
- https://docs.cursor.com/settings/api-keys
- https://docs.cursor.com/chat/overview

### Configuration fields

- **Cursor Settings → OpenAI API Key:** `gtak_...`
- **Cursor Settings → Override OpenAI Base URL:** `https://<tenant-host>/api/tenant`
- **Model name / alias mapping:** `published-coding-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Model picker uses published alias when override path is active |
| `POST /v1/chat/completions` | native | Supported Cursor chat modes posting to custom OpenAI base → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Not exposed in standard Cursor override configuration |
| `POST /v1/audio/transcriptions` | not_supported | Not supported via Cursor OpenAI override |
| `POST /v1/audio/speech` | not_supported | Not supported via Cursor OpenAI override |
| `POST /v1/images/generations` | not_supported | Not supported via Cursor OpenAI override |
| `POST /v1/conversations/files` | not_supported | Not applicable to editor workflow |
| `POST /v1/datasets/{id}/files` | not_supported | Not applicable to editor workflow |
| `GET /v1/files/{id}` | not_supported | Not applicable to editor workflow |

### Not supported in this product

- Cursor Agent and some Composer flows may not honor custom OpenAI base URLs — GT API applies to supported override paths only.
- Cursor-hosted models cannot be repointed to GT API without the override settings above.

### Prerequisites

- Confirm target Cursor build supports custom OpenAI base URL (not all Agent-only flows do).
- Create dedicated agentic-editor inference key.

### Setup steps

1. Cursor Settings → Models → paste GT API key and set Base URL to tenant GT API origin.
2. Select or map a published coding alias as the model name.
3. Run a low-risk workspace completion test.
4. Document that Agent/Composer features may still route through Cursor-hosted models.

### GT extensions and caveats

- Editor chat usually does not need GT conversation uploads.
- If wrapping GT behind another proxy, validate that layer separately.

### Validation checklist

- Configured alias produces valid completions in supported modes.
- Traffic uses dedicated key, not shared app key.
- Integration survives key rotation.

### Plain-text export

```text
Cursor runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

When the Cursor environment allows overriding the OpenAI API base URL, point it at GT API with a dedicated editor inference key and published coding alias.

Official documentation:
- https://docs.cursor.com/settings/models
- https://docs.cursor.com/settings/api-keys
- https://docs.cursor.com/chat/overview

Configuration fields:
- Cursor Settings → OpenAI API Key: gtak_...
- Cursor Settings → Override OpenAI Base URL: https://<tenant-host>/api/tenant
- Model name / alias mapping: published-coding-alias

GT route mapping:
- GET /v1/models (native): Model picker uses published alias when override path is active
- POST /v1/chat/completions (native): Supported Cursor chat modes posting to custom OpenAI base → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Not exposed in standard Cursor override configuration
- POST /v1/audio/transcriptions (not_supported): Not supported via Cursor OpenAI override
- POST /v1/audio/speech (not_supported): Not supported via Cursor OpenAI override
- POST /v1/images/generations (not_supported): Not supported via Cursor OpenAI override
- POST /v1/conversations/files (not_supported): Not applicable to editor workflow
- POST /v1/datasets/{id}/files (not_supported): Not applicable to editor workflow
- GET /v1/files/{id} (not_supported): Not applicable to editor workflow

Not supported in this product:
- Cursor Agent and some Composer flows may not honor custom OpenAI base URLs — GT API applies to supported override paths only.
- Cursor-hosted models cannot be repointed to GT API without the override settings above.

Prerequisites:
- Confirm target Cursor build supports custom OpenAI base URL (not all Agent-only flows do).
- Create dedicated agentic-editor inference key.

Setup steps:
1. Cursor Settings → Models → paste GT API key and set Base URL to tenant GT API origin.
2. Select or map a published coding alias as the model name.
3. Run a low-risk workspace completion test.
4. Document that Agent/Composer features may still route through Cursor-hosted models.

GT extensions and caveats:
- Editor chat usually does not need GT conversation uploads.
- If wrapping GT behind another proxy, validate that layer separately.

Validation checklist:
- Configured alias produces valid completions in supported modes.
- Traffic uses dedicated key, not shared app key.
- Integration survives key rotation.
```
