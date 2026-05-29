## Start Here

Configure LangChain OpenAI chat and embedding classes with the GT API base URL; keep GT conversation bootstrap and file ingestion in adjacent application code. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **LangChain** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** Framework and orchestration

### Official documentation

- https://python.langchain.com/docs/integrations/chat/openai/
- https://js.langchain.com/docs/integrations/chat/openai/
- https://python.langchain.com/docs/integrations/text_embedding/openai/

### Configuration fields

- **ChatOpenAI.base_url (Python):** `https://<tenant-host>/api/tenant`
- **ChatOpenAI.api_key:** `gtak_...`
- **OpenAIEmbeddings.base_url:** `https://<tenant-host>/api/tenant`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Implicit via configured `model` string; validate with a direct `GET /v1/models` curl during setup |
| `POST /v1/chat/completions` | native | ChatOpenAI invokes `POST /v1/chat/completions` through the OpenAI-compatible client |
| `POST /v1/embeddings` | native | OpenAIEmbeddings calls `POST /v1/embeddings` with the same published alias |
| `POST /v1/audio/transcriptions` | not_supported | Not exposed by default LangChain OpenAI chat integrations |
| `POST /v1/audio/speech` | not_supported | Not exposed by default LangChain OpenAI chat integrations |
| `POST /v1/images/generations` | not_supported | Use LangChain OpenAI image helpers only if you add explicit image-capable key scopes |
| `POST /v1/conversations/files` | gt_extension | Custom Python/JS HTTP client alongside the chain |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom ingestion script or tool calling GT multipart upload |
| `GET /v1/files/{id}` | gt_extension | Poll from wrapper code after upload |

### Not supported in this product

- LangChain built-in OpenAI Files API helpers target vendor file ids, not GT dataset or conversation upload routes.

### Prerequisites

- Publish agent aliases (and raw-model names if needed) for chain consumption.
- Create chat-plus-embeddings inference key when vector stores call `/v1/embeddings`.

### Setup steps

1. Set `base_url` / `baseURL` to the tenant GT API URL ending in `/api/tenant`.
2. Pass the GT API bearer key as `api_key` / `openAIApiKey`.
3. Use a published alias as the LangChain `model` parameter.
4. Wire `OpenAIEmbeddings` to the same base URL before enabling retrieval chains.

### GT extensions and caveats

- Call `POST /v1/conversations` from your app service when you need GT-managed continuity.
- Use explicit HTTP for `/v1/datasets/{id}/files` rather than assuming `DirectoryLoader` uploads to GT.

### Validation checklist

- Chain completes with OpenAI-shaped assistant content.
- Embedding batches succeed with the same alias boundary when enabled.
- Key rotation updates LangChain env/config without alias leakage.

### Plain-text export

```text
LangChain runbook
Native OpenAI-compatible · Framework and orchestration
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Configure LangChain OpenAI chat and embedding classes with the GT API base URL; keep GT conversation bootstrap and file ingestion in adjacent application code.

Official documentation:
- https://python.langchain.com/docs/integrations/chat/openai/
- https://js.langchain.com/docs/integrations/chat/openai/
- https://python.langchain.com/docs/integrations/text_embedding/openai/

Configuration fields:
- ChatOpenAI.base_url (Python): https://<tenant-host>/api/tenant
- ChatOpenAI.api_key: gtak_...
- OpenAIEmbeddings.base_url: https://<tenant-host>/api/tenant

GT route mapping:
- GET /v1/models (native): Implicit via configured `model` string; validate with a direct `GET /v1/models` curl during setup
- POST /v1/chat/completions (native): ChatOpenAI invokes `POST /v1/chat/completions` through the OpenAI-compatible client
- POST /v1/embeddings (native): OpenAIEmbeddings calls `POST /v1/embeddings` with the same published alias
- POST /v1/audio/transcriptions (not_supported): Not exposed by default LangChain OpenAI chat integrations
- POST /v1/audio/speech (not_supported): Not exposed by default LangChain OpenAI chat integrations
- POST /v1/images/generations (not_supported): Use LangChain OpenAI image helpers only if you add explicit image-capable key scopes
- POST /v1/conversations/files (gt_extension): Custom Python/JS HTTP client alongside the chain
- POST /v1/datasets/{id}/files (gt_extension): Custom ingestion script or tool calling GT multipart upload
- GET /v1/files/{id} (gt_extension): Poll from wrapper code after upload

Not supported in this product:
- LangChain built-in OpenAI Files API helpers target vendor file ids, not GT dataset or conversation upload routes.

Prerequisites:
- Publish agent aliases (and raw-model names if needed) for chain consumption.
- Create chat-plus-embeddings inference key when vector stores call `/v1/embeddings`.

Setup steps:
1. Set `base_url` / `baseURL` to the tenant GT API URL ending in `/api/tenant`.
2. Pass the GT API bearer key as `api_key` / `openAIApiKey`.
3. Use a published alias as the LangChain `model` parameter.
4. Wire `OpenAIEmbeddings` to the same base URL before enabling retrieval chains.

GT extensions and caveats:
- Call `POST /v1/conversations` from your app service when you need GT-managed continuity.
- Use explicit HTTP for `/v1/datasets/{id}/files` rather than assuming `DirectoryLoader` uploads to GT.

Validation checklist:
- Chain completes with OpenAI-shaped assistant content.
- Embedding batches succeed with the same alias boundary when enabled.
- Key rotation updates LangChain env/config without alias leakage.
```
