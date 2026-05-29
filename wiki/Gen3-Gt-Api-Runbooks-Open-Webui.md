## Start Here

Configure Open WebUI admin connection settings with GT API base URL (`OPENAI_API_BASE_URL`) and a scoped inference key; published aliases appear as selectable models. Recommended preset: **OpenAI-compatible chat client**.

## Why this matters

This runbook maps **Open WebUI** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Workflow and builders

### Official documentation

- https://docs.openwebui.com/getting-started/env-configuration/
- https://docs.openwebui.com/getting-started/quick-start/
- https://docs.openwebui.com/features/chat-features/

### Configuration fields

- **OPENAI_API_BASE_URL:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **Admin → Connections → OpenAI → API Base URL:** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Open WebUI model refresh calls `/v1/models` via configured base URL |
| `POST /v1/chat/completions` | native | Open WebUI chat → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | When embed scope on key and Open WebUI embed config uses same base |
| `POST /v1/audio/transcriptions` | not_supported | Not default Open WebUI OpenAI connection path |
| `POST /v1/audio/speech` | not_supported | Not default Open WebUI OpenAI connection path |
| `POST /v1/images/generations` | not_supported | Not default unless image features configured with GT image scope |
| `POST /v1/conversations/files` | not_supported | External script — not default UI attachment pipeline |
| `POST /v1/datasets/{id}/files` | not_supported | External ingestion automation to GT dataset route |
| `GET /v1/files/{id}` | not_supported | External polling after GT upload |

### Not supported in this product

- Open WebUI default file attachment flow is product-local, not GT conversation or dataset upload routes.

### Prerequisites

- Publish aliases chat users should see.
- Create inference key with chat (and embed if needed) scopes.

### Setup steps

1. Set `OPENAI_API_BASE_URL` to tenant GT API URL in container env or admin UI.
2. Paste GT API key into OpenAI connection settings.
3. Reload models and confirm only allowlisted published aliases appear.
4. Complete one user chat turn with a published alias.

### GT extensions and caveats

- Use separate automation for `/v1/datasets/{id}/files` — default UI attachments may not map to GT.
- Enable embed scope only when Open WebUI calls `/v1/embeddings` through GT.

### Validation checklist

- User completes chat with published alias.
- Model picker does not leak disallowed aliases.
- Key rotation documented for Open WebUI operators.

### Plain-text export

```text
Open WebUI runbook
Guided OpenAI-compatible setup · Workflow and builders
Recommended key preset: OpenAI-compatible chat client
Evidence: documented compatibility (vendor docs cross-check)

Configure Open WebUI admin connection settings with GT API base URL (`OPENAI_API_BASE_URL`) and a scoped inference key; published aliases appear as selectable models.

Official documentation:
- https://docs.openwebui.com/getting-started/env-configuration/
- https://docs.openwebui.com/getting-started/quick-start/
- https://docs.openwebui.com/features/chat-features/

Configuration fields:
- OPENAI_API_BASE_URL: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- Admin → Connections → OpenAI → API Base URL: https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): Open WebUI model refresh calls `/v1/models` via configured base URL
- POST /v1/chat/completions (native): Open WebUI chat → `/v1/chat/completions`
- POST /v1/embeddings (native): When embed scope on key and Open WebUI embed config uses same base
- POST /v1/audio/transcriptions (not_supported): Not default Open WebUI OpenAI connection path
- POST /v1/audio/speech (not_supported): Not default Open WebUI OpenAI connection path
- POST /v1/images/generations (not_supported): Not default unless image features configured with GT image scope
- POST /v1/conversations/files (not_supported): External script — not default UI attachment pipeline
- POST /v1/datasets/{id}/files (not_supported): External ingestion automation to GT dataset route
- GET /v1/files/{id} (not_supported): External polling after GT upload

Not supported in this product:
- Open WebUI default file attachment flow is product-local, not GT conversation or dataset upload routes.

Prerequisites:
- Publish aliases chat users should see.
- Create inference key with chat (and embed if needed) scopes.

Setup steps:
1. Set `OPENAI_API_BASE_URL` to tenant GT API URL in container env or admin UI.
2. Paste GT API key into OpenAI connection settings.
3. Reload models and confirm only allowlisted published aliases appear.
4. Complete one user chat turn with a published alias.

GT extensions and caveats:
- Use separate automation for `/v1/datasets/{id}/files` — default UI attachments may not map to GT.
- Enable embed scope only when Open WebUI calls `/v1/embeddings` through GT.

Validation checklist:
- User completes chat with published alias.
- Model picker does not leak disallowed aliases.
- Key rotation documented for Open WebUI operators.
```
