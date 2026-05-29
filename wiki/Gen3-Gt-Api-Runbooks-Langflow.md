## Start Here

Configure Langflow OpenAI chat components with the GT base URL; add HTTP Request nodes for GT conversation bootstrap, dataset uploads, and file-status polling. Recommended preset: **Conversation app with uploads**.

## Why this matters

This runbook maps **Langflow** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Workflow and builders

### Official documentation

- https://docs.langflow.org/components-models
- https://docs.langflow.org/configuration-global-vars
- https://docs.langflow.org/components-data#http-request

### Configuration fields

- **OpenAI component → OpenAI API Base:** `https://<tenant-host>/api/tenant`
- **OpenAI component → API Key:** `gtak_...`
- **Global variable LANGFLOW_OPENAI_API_BASE (optional):** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Set model field to published alias; optional HTTP node to list models during setup |
| `POST /v1/chat/completions` | native | Langflow OpenAI chat component → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | OpenAI embeddings component when flow includes embed scope on key |
| `POST /v1/audio/transcriptions` | not_supported | No default Langflow OpenAI audio component for custom GT base |
| `POST /v1/audio/speech` | not_supported | No default Langflow OpenAI audio component for custom GT base |
| `POST /v1/images/generations` | not_supported | Requires dedicated image component + GT image scope if used |
| `POST /v1/conversations/files` | gt_extension | HTTP Request multipart node to `/v1/conversations/files` |
| `POST /v1/datasets/{id}/files` | gt_extension | HTTP Request multipart to `/v1/datasets/{id}/files` |
| `GET /v1/files/{id}` | gt_extension | HTTP Request GET `/v1/files/{id}` poll loop |

### Not supported in this product

- Langflow OpenAI file components target vendor OpenAI Files, not GT dataset or conversation upload routes.

### Prerequisites

- Choose inference-only, dataset-upload, or conversation-plus-upload preset before building the flow.
- Publish aliases referenced in OpenAI component model fields.

### Setup steps

1. Open Langflow → add OpenAI model component → set API Base URL to `/api/tenant` on tenant host.
2. Paste GT bearer key into component API key field or linked secret.
3. Set model name to a published alias from `GET /v1/models`.
4. Add HTTP Request nodes for `POST /v1/conversations`, uploads, and `GET /v1/files/{id}` when needed.

### GT extensions and caveats

- Persist `X-GT-Conversation-Id` in Langflow session or component state between nodes.
- Switch to dataset-upload preset when the flow only ingests into fixed datasets.

### Validation checklist

- OpenAI component completes a chat turn with the published alias.
- HTTP nodes succeed with the same bearer key and GT headers.
- Upload + poll visible in Langflow execution logs.

### Plain-text export

```text
Langflow runbook
Guided OpenAI-compatible setup · Workflow and builders
Recommended key preset: Conversation app with uploads
Evidence: documented compatibility (vendor docs cross-check)

Configure Langflow OpenAI chat components with the GT base URL; add HTTP Request nodes for GT conversation bootstrap, dataset uploads, and file-status polling.

Official documentation:
- https://docs.langflow.org/components-models
- https://docs.langflow.org/configuration-global-vars
- https://docs.langflow.org/components-data#http-request

Configuration fields:
- OpenAI component → OpenAI API Base: https://<tenant-host>/api/tenant
- OpenAI component → API Key: gtak_...
- Global variable LANGFLOW_OPENAI_API_BASE (optional): https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): Set model field to published alias; optional HTTP node to list models during setup
- POST /v1/chat/completions (native): Langflow OpenAI chat component → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): OpenAI embeddings component when flow includes embed scope on key
- POST /v1/audio/transcriptions (not_supported): No default Langflow OpenAI audio component for custom GT base
- POST /v1/audio/speech (not_supported): No default Langflow OpenAI audio component for custom GT base
- POST /v1/images/generations (not_supported): Requires dedicated image component + GT image scope if used
- POST /v1/conversations/files (gt_extension): HTTP Request multipart node to `/v1/conversations/files`
- POST /v1/datasets/{id}/files (gt_extension): HTTP Request multipart to `/v1/datasets/{id}/files`
- GET /v1/files/{id} (gt_extension): HTTP Request GET `/v1/files/{id}` poll loop

Not supported in this product:
- Langflow OpenAI file components target vendor OpenAI Files, not GT dataset or conversation upload routes.

Prerequisites:
- Choose inference-only, dataset-upload, or conversation-plus-upload preset before building the flow.
- Publish aliases referenced in OpenAI component model fields.

Setup steps:
1. Open Langflow → add OpenAI model component → set API Base URL to `/api/tenant` on tenant host.
2. Paste GT bearer key into component API key field or linked secret.
3. Set model name to a published alias from `GET /v1/models`.
4. Add HTTP Request nodes for `POST /v1/conversations`, uploads, and `GET /v1/files/{id}` when needed.

GT extensions and caveats:
- Persist `X-GT-Conversation-Id` in Langflow session or component state between nodes.
- Switch to dataset-upload preset when the flow only ingests into fixed datasets.

Validation checklist:
- OpenAI component completes a chat turn with the published alias.
- HTTP nodes succeed with the same bearer key and GT headers.
- Upload + poll visible in Langflow execution logs.
```
