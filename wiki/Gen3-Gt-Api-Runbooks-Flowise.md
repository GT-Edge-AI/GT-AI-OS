## Start Here

Set Flowise ChatOpenAI nodes to the GT API base path with bearer credentials; use Custom Tool or HTTP nodes for GT-only conversation and upload routes. Recommended preset: **Conversation app with uploads**.

## Why this matters

This runbook maps **Flowise** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Workflow and builders

### Official documentation

- https://docs.flowiseai.com/configuration/environment-variables
- https://docs.flowiseai.com/integrations/langchain/chat-models/chat-openai
- https://docs.flowiseai.com/using-flowise/agentflows

### Configuration fields

- **ChatOpenAI → Base Path:** `https://<tenant-host>/api/tenant`
- **Credentials → openAIApiKey:** `gtak_...`
- **ChatOpenAI → Model Name:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Model Name field must match published alias; confirm via setup curl to `/v1/models` |
| `POST /v1/chat/completions` | native | ChatOpenAI node posts to GT `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | OpenAI Embeddings node when key includes embed scope |
| `POST /v1/audio/transcriptions` | not_supported | Not available in default Flowise OpenAI chat nodes |
| `POST /v1/audio/speech` | not_supported | Not available in default Flowise OpenAI chat nodes |
| `POST /v1/images/generations` | not_supported | Not default unless image-specific node added with GT image scope |
| `POST /v1/conversations/files` | gt_extension | Custom Tool HTTP multipart to conversation files route |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom Tool HTTP multipart to dataset files route |
| `GET /v1/files/{id}` | gt_extension | Custom Tool GET poll on file id |

### Not supported in this product

- Flowise document store loaders do not automatically upload into GT dataset routes.

### Prerequisites

- Decide chat-only vs conversation-plus-upload before selecting key preset.
- Publish aliases used in ChatOpenAI model name fields.

### Setup steps

1. Flowise Credentials → add OpenAI API credential with GT key.
2. ChatOpenAI node → Base Path `https://<tenant-host>/api/tenant`, select credential, set Model Name to published alias.
3. Validate one chatflow execution before enabling agents with tools.
4. Add Custom Tool node calling GT HTTP routes when uploads or conversations are required.

### GT extensions and caveats

- Store conversation id in Flowise **Variable** node output for downstream chat/upload nodes.
- Use dataset-upload preset for ingestion-only automations.

### Validation checklist

- ChatOpenAI node returns assistant content with GT alias.
- Custom Tool/HTTP nodes authenticate with the same GT key.
- Execution history shows upload polling when enabled.

### Plain-text export

```text
Flowise runbook
Guided OpenAI-compatible setup · Workflow and builders
Recommended key preset: Conversation app with uploads
Evidence: documented compatibility (vendor docs cross-check)

Set Flowise ChatOpenAI nodes to the GT API base path with bearer credentials; use Custom Tool or HTTP nodes for GT-only conversation and upload routes.

Official documentation:
- https://docs.flowiseai.com/configuration/environment-variables
- https://docs.flowiseai.com/integrations/langchain/chat-models/chat-openai
- https://docs.flowiseai.com/using-flowise/agentflows

Configuration fields:
- ChatOpenAI → Base Path: https://<tenant-host>/api/tenant
- Credentials → openAIApiKey: gtak_...
- ChatOpenAI → Model Name: published-agent-alias

GT route mapping:
- GET /v1/models (native): Model Name field must match published alias; confirm via setup curl to `/v1/models`
- POST /v1/chat/completions (native): ChatOpenAI node posts to GT `/v1/chat/completions`
- POST /v1/embeddings (not_supported): OpenAI Embeddings node when key includes embed scope
- POST /v1/audio/transcriptions (not_supported): Not available in default Flowise OpenAI chat nodes
- POST /v1/audio/speech (not_supported): Not available in default Flowise OpenAI chat nodes
- POST /v1/images/generations (not_supported): Not default unless image-specific node added with GT image scope
- POST /v1/conversations/files (gt_extension): Custom Tool HTTP multipart to conversation files route
- POST /v1/datasets/{id}/files (gt_extension): Custom Tool HTTP multipart to dataset files route
- GET /v1/files/{id} (gt_extension): Custom Tool GET poll on file id

Not supported in this product:
- Flowise document store loaders do not automatically upload into GT dataset routes.

Prerequisites:
- Decide chat-only vs conversation-plus-upload before selecting key preset.
- Publish aliases used in ChatOpenAI model name fields.

Setup steps:
1. Flowise Credentials → add OpenAI API credential with GT key.
2. ChatOpenAI node → Base Path `https://<tenant-host>/api/tenant`, select credential, set Model Name to published alias.
3. Validate one chatflow execution before enabling agents with tools.
4. Add Custom Tool node calling GT HTTP routes when uploads or conversations are required.

GT extensions and caveats:
- Store conversation id in Flowise **Variable** node output for downstream chat/upload nodes.
- Use dataset-upload preset for ingestion-only automations.

Validation checklist:
- ChatOpenAI node returns assistant content with GT alias.
- Custom Tool/HTTP nodes authenticate with the same GT key.
- Execution history shows upload polling when enabled.
```
