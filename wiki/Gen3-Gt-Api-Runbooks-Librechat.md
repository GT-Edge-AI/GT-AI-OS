## Start Here

Point LibreChat custom OpenAI endpoints at GT API via `librechat.yaml` and environment secrets; bind custom model entries to published agent aliases. Recommended preset: **OpenAI-compatible chat client**.

## Why this matters

This runbook maps **LibreChat** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Workflow and builders

### Official documentation

- https://www.librechat.ai/docs/configuration/librechat_yaml/ai_endpoints
- https://www.librechat.ai/docs/configuration/dotenv
- https://www.librechat.ai/docs/configuration/librechat_yaml/object_structure/custom_endpoint

### Configuration fields

- **OPENAI_REVERSE_PROXY:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **librechat.yaml → endpoints.custom[].baseURL:** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | LibreChat custom endpoint model list or fetch against `/v1/models` |
| `POST /v1/chat/completions` | native | LibreChat OpenAI client → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | When embed scope enabled and LibreChat routes embed calls to same proxy |
| `POST /v1/audio/transcriptions` | not_supported | Not default LibreChat custom OpenAI endpoint path |
| `POST /v1/audio/speech` | not_supported | Not default LibreChat custom OpenAI endpoint path |
| `POST /v1/images/generations` | not_supported | Not default unless image endpoint configured with GT image scope |
| `POST /v1/conversations/files` | not_supported | Custom middleware HTTP multipart — not default LibreChat files |
| `POST /v1/datasets/{id}/files` | not_supported | Custom middleware to GT dataset upload route |
| `GET /v1/files/{id}` | not_supported | Custom middleware GET poll |

### Not supported in this product

- LibreChat native file upload UX does not map to GT dataset or conversation multipart routes without custom middleware.

### Prerequisites

- Decide which deployment personas need GT access.
- Create one inference key per environment for hard isolation if needed.

### Setup steps

1. Configure OpenAI-compatible endpoint URL to tenant GT API base in `librechat.yaml` or env.
2. Store GT API key in LibreChat secrets/env as documented.
3. Map selectable model names to published aliases.
4. Validate first chat completion end-to-end.

### GT extensions and caveats

- GT conversation bootstrap as custom middleware if persisted GT threads are required.
- Use chat-plus-embeddings preset when embedding calls route through GT.

### Validation checklist

- Chat works with published alias.
- Internal endpoints not exposed in model lists.
- Credential rotation does not break unrelated LibreChat providers.

### Plain-text export

```text
LibreChat runbook
Guided OpenAI-compatible setup · Workflow and builders
Recommended key preset: OpenAI-compatible chat client
Evidence: documented compatibility (vendor docs cross-check)

Point LibreChat custom OpenAI endpoints at GT API via `librechat.yaml` and environment secrets; bind custom model entries to published agent aliases.

Official documentation:
- https://www.librechat.ai/docs/configuration/librechat_yaml/ai_endpoints
- https://www.librechat.ai/docs/configuration/dotenv
- https://www.librechat.ai/docs/configuration/librechat_yaml/object_structure/custom_endpoint

Configuration fields:
- OPENAI_REVERSE_PROXY: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- librechat.yaml → endpoints.custom[].baseURL: https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): LibreChat custom endpoint model list or fetch against `/v1/models`
- POST /v1/chat/completions (native): LibreChat OpenAI client → `/v1/chat/completions`
- POST /v1/embeddings (native): When embed scope enabled and LibreChat routes embed calls to same proxy
- POST /v1/audio/transcriptions (not_supported): Not default LibreChat custom OpenAI endpoint path
- POST /v1/audio/speech (not_supported): Not default LibreChat custom OpenAI endpoint path
- POST /v1/images/generations (not_supported): Not default unless image endpoint configured with GT image scope
- POST /v1/conversations/files (not_supported): Custom middleware HTTP multipart — not default LibreChat files
- POST /v1/datasets/{id}/files (not_supported): Custom middleware to GT dataset upload route
- GET /v1/files/{id} (not_supported): Custom middleware GET poll

Not supported in this product:
- LibreChat native file upload UX does not map to GT dataset or conversation multipart routes without custom middleware.

Prerequisites:
- Decide which deployment personas need GT access.
- Create one inference key per environment for hard isolation if needed.

Setup steps:
1. Configure OpenAI-compatible endpoint URL to tenant GT API base in `librechat.yaml` or env.
2. Store GT API key in LibreChat secrets/env as documented.
3. Map selectable model names to published aliases.
4. Validate first chat completion end-to-end.

GT extensions and caveats:
- GT conversation bootstrap as custom middleware if persisted GT threads are required.
- Use chat-plus-embeddings preset when embedding calls route through GT.

Validation checklist:
- Chat works with published alias.
- Internal endpoints not exposed in model lists.
- Credential rotation does not break unrelated LibreChat providers.
```
