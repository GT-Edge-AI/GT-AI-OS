## Start Here

Add an OpenAI-API-compatible model provider in Dify pointed at GT API for chat and embeddings; implement GT upload and conversation routes as explicit HTTP workflow steps. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **Dify** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Workflow and builders

### Official documentation

- https://docs.dify.ai/guides/model-configuration/openai
- https://docs.dify.ai/guides/workflow/node/llm
- https://docs.dify.ai/guides/workflow/node/http-request

### Configuration fields

- **OpenAI-API-compatible → API Base URL:** `https://<tenant-host>/api/tenant`
- **OpenAI-API-compatible → API Key:** `gtak_...`
- **LLM node → Model (published alias):** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Dify provider test + manual `GET /v1/models` during provider setup |
| `POST /v1/chat/completions` | native | App/workflow LLM node → `/v1/chat/completions` via OpenAI-compatible provider |
| `POST /v1/embeddings` | native | Embedding model selection through same provider → `/v1/embeddings` |
| `POST /v1/audio/transcriptions` | not_supported | Not exposed through Dify OpenAI-compatible provider by default |
| `POST /v1/audio/speech` | not_supported | Not exposed through Dify OpenAI-compatible provider by default |
| `POST /v1/images/generations` | not_supported | Requires image-capable published target and GT image scope if used |
| `POST /v1/conversations/files` | gt_extension | Workflow HTTP Request multipart with GT conversation header |
| `POST /v1/datasets/{id}/files` | gt_extension | Workflow HTTP Request to dataset files route |
| `GET /v1/files/{id}` | gt_extension | Workflow HTTP GET poll on file id |

### Not supported in this product

- Dify vendor-native OpenAI file and assistant APIs do not map to GT dataset or conversation upload semantics.

### Prerequisites

- Publish aliases for Dify apps and workflows.
- Grant `inference:chat` and `inference:embed` on key when knowledge/RAG uses GT embeddings.

### Setup steps

1. Dify console → Model Provider → OpenAI-API-compatible → set Base URL to tenant GT API.
2. Paste GT API key and save provider credentials.
3. Select a published alias in an app LLM node; run test completion.
4. Add HTTP Request node in workflows for GT conversation bootstrap or dataset uploads when required.

### GT extensions and caveats

- Call `POST /v1/conversations` from a workflow tool you control, not from default OpenAI provider shortcuts.
- Use `/v1/datasets/{id}/files` from HTTP nodes — Dify native file APIs are not GT dataset routes.

### Validation checklist

- Chat and embedding nodes succeed with expected aliases.
- Knowledge features still work after credential rotation.
- GT-only steps are documented for operators, not hidden behind failing provider assumptions.

### Plain-text export

```text
Dify runbook
OpenAI plus GT extensions · Workflow and builders
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Add an OpenAI-API-compatible model provider in Dify pointed at GT API for chat and embeddings; implement GT upload and conversation routes as explicit HTTP workflow steps.

Official documentation:
- https://docs.dify.ai/guides/model-configuration/openai
- https://docs.dify.ai/guides/workflow/node/llm
- https://docs.dify.ai/guides/workflow/node/http-request

Configuration fields:
- OpenAI-API-compatible → API Base URL: https://<tenant-host>/api/tenant
- OpenAI-API-compatible → API Key: gtak_...
- LLM node → Model (published alias): published-agent-alias

GT route mapping:
- GET /v1/models (native): Dify provider test + manual `GET /v1/models` during provider setup
- POST /v1/chat/completions (native): App/workflow LLM node → `/v1/chat/completions` via OpenAI-compatible provider
- POST /v1/embeddings (native): Embedding model selection through same provider → `/v1/embeddings`
- POST /v1/audio/transcriptions (not_supported): Not exposed through Dify OpenAI-compatible provider by default
- POST /v1/audio/speech (not_supported): Not exposed through Dify OpenAI-compatible provider by default
- POST /v1/images/generations (not_supported): Requires image-capable published target and GT image scope if used
- POST /v1/conversations/files (gt_extension): Workflow HTTP Request multipart with GT conversation header
- POST /v1/datasets/{id}/files (gt_extension): Workflow HTTP Request to dataset files route
- GET /v1/files/{id} (gt_extension): Workflow HTTP GET poll on file id

Not supported in this product:
- Dify vendor-native OpenAI file and assistant APIs do not map to GT dataset or conversation upload semantics.

Prerequisites:
- Publish aliases for Dify apps and workflows.
- Grant `inference:chat` and `inference:embed` on key when knowledge/RAG uses GT embeddings.

Setup steps:
1. Dify console → Model Provider → OpenAI-API-compatible → set Base URL to tenant GT API.
2. Paste GT API key and save provider credentials.
3. Select a published alias in an app LLM node; run test completion.
4. Add HTTP Request node in workflows for GT conversation bootstrap or dataset uploads when required.

GT extensions and caveats:
- Call `POST /v1/conversations` from a workflow tool you control, not from default OpenAI provider shortcuts.
- Use `/v1/datasets/{id}/files` from HTTP nodes — Dify native file APIs are not GT dataset routes.

Validation checklist:
- Chat and embedding nodes succeed with expected aliases.
- Knowledge features still work after credential rotation.
- GT-only steps are documented for operators, not hidden behind failing provider assumptions.
```
