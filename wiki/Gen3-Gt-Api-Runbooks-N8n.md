## Start Here

Use n8n OpenAI-compatible nodes for chat against GT API and HTTP Request nodes for GT conversation bootstrap, dataset uploads, and file-status polling. Recommended preset: **Dataset upload automation**.

## Why this matters

This runbook maps **n8n** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Workflow and builders

### Official documentation

- https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/
- https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/
- https://docs.n8n.io/credentials/openai/

### Configuration fields

- **OpenAI credentials → API Key:** `gtak_...`
- **OpenAI node → Base URL (override):** `https://<tenant-host>/api/tenant`
- **HTTP Request → Header Authorization:** `Bearer gtak_...`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | OpenAI node model field = published alias; optional HTTP GET `/v1/models` node |
| `POST /v1/chat/completions` | native | OpenAI / LangChain OpenAI node → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | OpenAI Embeddings node when key includes embed scope |
| `POST /v1/audio/transcriptions` | not_supported | Not default n8n OpenAI node path for GT |
| `POST /v1/audio/speech` | not_supported | Not default n8n OpenAI node path for GT |
| `POST /v1/images/generations` | not_supported | OpenAI Image node only with GT image scope on key |
| `POST /v1/conversations/files` | gt_extension | HTTP Request multipart POST to `/v1/conversations/files` |
| `POST /v1/datasets/{id}/files` | gt_extension | HTTP Request multipart POST to `/v1/datasets/{id}/files` |
| `GET /v1/files/{id}` | gt_extension | HTTP Request GET `/v1/files/{id}` poll loop |

### Not supported in this product

- n8n OpenAI node does not automatically attach GT conversation headers or dataset multipart semantics.

### Prerequisites

- Decide chat-only, dataset upload, or conversation-plus-upload workflow.
- Create matching key preset before building workflow.

### Setup steps

1. Add OpenAI node → Credentials → API Key = GT key; Base URL = tenant GT API.
2. Set model to published alias; test chat completion execution.
3. Add HTTP Request nodes for GT routes (conversations, uploads, file status) with same bearer credential.
4. Store GT conversation id in workflow static data when continuity is required.

### GT extensions and caveats

- Dataset upload keys best for ingestion-only automations.
- Conversation app keys when one workflow needs chat plus conversation-scoped files.

### Validation checklist

- OpenAI node succeeds with published alias.
- HTTP nodes upload and poll file to `ready`.
- GT conversation id persisted and reused in workflow state.

### Plain-text export

```text
n8n runbook
OpenAI plus GT extensions · Workflow and builders
Recommended key preset: Dataset upload automation
Evidence: documented compatibility (vendor docs cross-check)

Use n8n OpenAI-compatible nodes for chat against GT API and HTTP Request nodes for GT conversation bootstrap, dataset uploads, and file-status polling.

Official documentation:
- https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/
- https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/
- https://docs.n8n.io/credentials/openai/

Configuration fields:
- OpenAI credentials → API Key: gtak_...
- OpenAI node → Base URL (override): https://<tenant-host>/api/tenant
- HTTP Request → Header Authorization: Bearer gtak_...

GT route mapping:
- GET /v1/models (native): OpenAI node model field = published alias; optional HTTP GET `/v1/models` node
- POST /v1/chat/completions (native): OpenAI / LangChain OpenAI node → `/v1/chat/completions`
- POST /v1/embeddings (native): OpenAI Embeddings node when key includes embed scope
- POST /v1/audio/transcriptions (not_supported): Not default n8n OpenAI node path for GT
- POST /v1/audio/speech (not_supported): Not default n8n OpenAI node path for GT
- POST /v1/images/generations (not_supported): OpenAI Image node only with GT image scope on key
- POST /v1/conversations/files (gt_extension): HTTP Request multipart POST to `/v1/conversations/files`
- POST /v1/datasets/{id}/files (gt_extension): HTTP Request multipart POST to `/v1/datasets/{id}/files`
- GET /v1/files/{id} (gt_extension): HTTP Request GET `/v1/files/{id}` poll loop

Not supported in this product:
- n8n OpenAI node does not automatically attach GT conversation headers or dataset multipart semantics.

Prerequisites:
- Decide chat-only, dataset upload, or conversation-plus-upload workflow.
- Create matching key preset before building workflow.

Setup steps:
1. Add OpenAI node → Credentials → API Key = GT key; Base URL = tenant GT API.
2. Set model to published alias; test chat completion execution.
3. Add HTTP Request nodes for GT routes (conversations, uploads, file status) with same bearer credential.
4. Store GT conversation id in workflow static data when continuity is required.

GT extensions and caveats:
- Dataset upload keys best for ingestion-only automations.
- Conversation app keys when one workflow needs chat plus conversation-scoped files.

Validation checklist:
- OpenAI node succeeds with published alias.
- HTTP nodes upload and poll file to `ready`.
- GT conversation id persisted and reused in workflow state.
```
