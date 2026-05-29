## Start Here

Golden-path compatibility: point any OpenAI SDK or curl client at the tenant GT API base URL with a scoped bearer key; model discovery lists published agent aliases and raw-model catalog names allowlisted on the key. Recommended preset: **OpenAI-compatible chat client**.

## Why this matters

This runbook maps **OpenAI SDK / curl** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** SDK and HTTP

### Official documentation

- https://platform.openai.com/docs/api-reference/introduction
- https://github.com/openai/openai-python
- https://github.com/openai/openai-node

### Configuration fields

- **OPENAI_BASE_URL / baseURL:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY / apiKey:** `gtak_...`
- **model (chat body):** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | OpenAI SDK `client.models.list()` or curl `GET {base}/v1/models` |
| `POST /v1/chat/completions` | native | OpenAI SDK `chat.completions.create()` or curl POST with JSON body |
| `POST /v1/embeddings` | native | OpenAI SDK `embeddings.create()` when key includes `inference:embed` |
| `POST /v1/audio/transcriptions` | native | OpenAI SDK `audio.transcriptions.create()` with multipart when key includes `inference:transcribe` |
| `POST /v1/audio/speech` | native | OpenAI SDK `audio.speech.create()` when key includes `inference:speech` |
| `POST /v1/images/generations` | native | OpenAI SDK `images.generate()` when key includes `inference:image` |
| `POST /v1/conversations/files` | gt_extension | Direct HTTP multipart to `/v1/conversations/files` with conversation header |
| `POST /v1/datasets/{id}/files` | gt_extension | Direct HTTP multipart to `/v1/datasets/{datasetId}/files` |
| `GET /v1/files/{id}` | gt_extension | Direct HTTP `GET /v1/files/{fileId}` polling loop |

### Not supported in this product

_None documented for this product._

### Prerequisites

- Publish at least one inference target (agent alias and/or raw-model catalog entry).
- Create an inference key with the scopes and allowlists the integration needs.

### Setup steps

1. Set base URL to https://<tenant-host>/api/tenant (no trailing slash on the /v1 segment — SDKs append route paths).
2. Set `Authorization: Bearer <gtak_...>` on every request (SDKs send this via `api_key` / `apiKey`).
3. Run `GET /v1/models` and confirm only intended published names appear.
4. Send a minimal `POST /v1/chat/completions` with `"model": "<published-name>"` and one user message.

### GT extensions and caveats

- Bootstrap GT-managed threads with `POST /v1/conversations`, then pass `X-GT-Conversation-Id` on follow-up chat and upload calls.
- Upload via `POST /v1/datasets/{id}/files` or `POST /v1/conversations/files`; poll `GET /v1/files/{id}` until status is `ready`.

### Validation checklist

- Model list matches key allowlists (no leaked unpublished aliases).
- Chat completion succeeds without exposing raw provider model ids.
- Optional: upload + poll reaches `ready` when upload scopes are enabled.

### Plain-text export

```text
OpenAI SDK / curl runbook
Native OpenAI-compatible · SDK and HTTP
Recommended key preset: OpenAI-compatible chat client
Evidence: deployed E2E verified (OpenAI SDK/curl golden path)

Golden-path compatibility: point any OpenAI SDK or curl client at the tenant GT API base URL with a scoped bearer key; model discovery lists published agent aliases and raw-model catalog names allowlisted on the key.

Official documentation:
- https://platform.openai.com/docs/api-reference/introduction
- https://github.com/openai/openai-python
- https://github.com/openai/openai-node

Configuration fields:
- OPENAI_BASE_URL / baseURL: https://<tenant-host>/api/tenant
- OPENAI_API_KEY / apiKey: gtak_...
- model (chat body): published-agent-alias

GT route mapping:
- GET /v1/models (native): OpenAI SDK `client.models.list()` or curl `GET {base}/v1/models`
- POST /v1/chat/completions (native): OpenAI SDK `chat.completions.create()` or curl POST with JSON body
- POST /v1/embeddings (native): OpenAI SDK `embeddings.create()` when key includes `inference:embed`
- POST /v1/audio/transcriptions (native): OpenAI SDK `audio.transcriptions.create()` with multipart when key includes `inference:transcribe`
- POST /v1/audio/speech (native): OpenAI SDK `audio.speech.create()` when key includes `inference:speech`
- POST /v1/images/generations (native): OpenAI SDK `images.generate()` when key includes `inference:image`
- POST /v1/conversations/files (gt_extension): Direct HTTP multipart to `/v1/conversations/files` with conversation header
- POST /v1/datasets/{id}/files (gt_extension): Direct HTTP multipart to `/v1/datasets/{datasetId}/files`
- GET /v1/files/{id} (gt_extension): Direct HTTP `GET /v1/files/{fileId}` polling loop

Prerequisites:
- Publish at least one inference target (agent alias and/or raw-model catalog entry).
- Create an inference key with the scopes and allowlists the integration needs.

Setup steps:
1. Set base URL to https://<tenant-host>/api/tenant (no trailing slash on the /v1 segment — SDKs append route paths).
2. Set `Authorization: Bearer <gtak_...>` on every request (SDKs send this via `api_key` / `apiKey`).
3. Run `GET /v1/models` and confirm only intended published names appear.
4. Send a minimal `POST /v1/chat/completions` with `"model": "<published-name>"` and one user message.

GT extensions and caveats:
- Bootstrap GT-managed threads with `POST /v1/conversations`, then pass `X-GT-Conversation-Id` on follow-up chat and upload calls.
- Upload via `POST /v1/datasets/{id}/files` or `POST /v1/conversations/files`; poll `GET /v1/files/{id}` until status is `ready`.

Validation checklist:
- Model list matches key allowlists (no leaked unpublished aliases).
- Chat completion succeeds without exposing raw provider model ids.
- Optional: upload + poll reaches `ready` when upload scopes are enabled.
```
