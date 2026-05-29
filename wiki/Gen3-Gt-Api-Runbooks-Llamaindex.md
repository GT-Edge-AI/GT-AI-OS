## Start Here

Treat GT API as the OpenAI-compatible LLM and embedding backend for LlamaIndex; orchestrate GT-specific uploads and conversations in host application code. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **LlamaIndex** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** Framework and orchestration

### Official documentation

- https://docs.llamaindex.ai/en/stable/api_reference/llms/openai/
- https://docs.llamaindex.ai/en/stable/examples/embeddings/OpenAI/
- https://docs.llamaindex.ai/en/stable/module_guides/models/llms/

### Configuration fields

- **OpenAI.api_base / OpenAILike.api_base:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **OpenAIEmbedding.api_base:** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Configured model name must match a published alias; confirm with manual `GET /v1/models` |
| `POST /v1/chat/completions` | native | OpenAI LLM / OpenAILike issues chat completion requests to GT |
| `POST /v1/embeddings` | native | OpenAIEmbedding batch calls to `/v1/embeddings` |
| `POST /v1/audio/transcriptions` | not_supported | No default LlamaIndex OpenAI audio integration against custom base URLs |
| `POST /v1/audio/speech` | not_supported | No default LlamaIndex OpenAI TTS integration against custom base URLs |
| `POST /v1/images/generations` | not_supported | Not part of standard LlamaIndex OpenAI LLM setup |
| `POST /v1/conversations/files` | gt_extension | Host app HTTP multipart with GT conversation header |
| `POST /v1/datasets/{id}/files` | gt_extension | Separate ingestion job targeting `/v1/datasets/{id}/files` |
| `GET /v1/files/{id}` | gt_extension | Host app polling after GT upload |

### Not supported in this product

- LlamaIndex data connectors do not natively upload into GT dataset routes.

### Prerequisites

- Publish aliases LlamaIndex pipelines should target.
- Issue chat-plus-embeddings key when both LLM and embedding stages use GT.

### Setup steps

1. Configure `api_base` / `base_url` on OpenAI LLM and embedding classes to `/api/tenant`.
2. Supply GT bearer key via `api_key` environment or constructor.
3. Select a published alias as the external model name in query engines.
4. Validate a single-query RAG path before enabling agents or multi-step workflows.

### GT extensions and caveats

- Persist GT conversation ids in your service layer, not inside LlamaIndex storage abstractions.
- Ingest documents to GT datasets with direct HTTP uploads before indexing if tenant RAG should use GT-managed corpora.

### Validation checklist

- Query engine returns answers using the published alias.
- Embedding calls succeed when `inference:embed` is on the key.
- No unexpected model names appear when you re-run model discovery manually.

### Plain-text export

```text
LlamaIndex runbook
Native OpenAI-compatible · Framework and orchestration
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Treat GT API as the OpenAI-compatible LLM and embedding backend for LlamaIndex; orchestrate GT-specific uploads and conversations in host application code.

Official documentation:
- https://docs.llamaindex.ai/en/stable/api_reference/llms/openai/
- https://docs.llamaindex.ai/en/stable/examples/embeddings/OpenAI/
- https://docs.llamaindex.ai/en/stable/module_guides/models/llms/

Configuration fields:
- OpenAI.api_base / OpenAILike.api_base: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- OpenAIEmbedding.api_base: https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): Configured model name must match a published alias; confirm with manual `GET /v1/models`
- POST /v1/chat/completions (native): OpenAI LLM / OpenAILike issues chat completion requests to GT
- POST /v1/embeddings (native): OpenAIEmbedding batch calls to `/v1/embeddings`
- POST /v1/audio/transcriptions (not_supported): No default LlamaIndex OpenAI audio integration against custom base URLs
- POST /v1/audio/speech (not_supported): No default LlamaIndex OpenAI TTS integration against custom base URLs
- POST /v1/images/generations (not_supported): Not part of standard LlamaIndex OpenAI LLM setup
- POST /v1/conversations/files (gt_extension): Host app HTTP multipart with GT conversation header
- POST /v1/datasets/{id}/files (gt_extension): Separate ingestion job targeting `/v1/datasets/{id}/files`
- GET /v1/files/{id} (gt_extension): Host app polling after GT upload

Not supported in this product:
- LlamaIndex data connectors do not natively upload into GT dataset routes.

Prerequisites:
- Publish aliases LlamaIndex pipelines should target.
- Issue chat-plus-embeddings key when both LLM and embedding stages use GT.

Setup steps:
1. Configure `api_base` / `base_url` on OpenAI LLM and embedding classes to `/api/tenant`.
2. Supply GT bearer key via `api_key` environment or constructor.
3. Select a published alias as the external model name in query engines.
4. Validate a single-query RAG path before enabling agents or multi-step workflows.

GT extensions and caveats:
- Persist GT conversation ids in your service layer, not inside LlamaIndex storage abstractions.
- Ingest documents to GT datasets with direct HTTP uploads before indexing if tenant RAG should use GT-managed corpora.

Validation checklist:
- Query engine returns answers using the published alias.
- Embedding calls succeed when `inference:embed` is on the key.
- No unexpected model names appear when you re-run model discovery manually.
```
