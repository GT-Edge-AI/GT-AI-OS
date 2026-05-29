## Start Here

Point Semantic Kernel OpenAI chat and embedding connectors at GT API; implement GT upload and conversation bootstrap in custom plugins or host services. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **Semantic Kernel** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Framework and orchestration

### Official documentation

- https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/chat-completion/
- https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.connectors.openai.openaichatcompletionservice
- https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/embedding-generation

### Configuration fields

- **OpenAIChatCompletionService endpoint (C#):** `https://<tenant-host>/api/tenant`
- **ApiKey / OPENAI_API_KEY:** `gtak_...`
- **ModelId in kernel prompt:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | ModelId must match published alias; validate with manual model list during setup |
| `POST /v1/chat/completions` | native | OpenAIChatCompletionService → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | OpenAITextEmbeddingGenerationService → `/v1/embeddings` |
| `POST /v1/audio/transcriptions` | not_supported | Not part of standard SK OpenAI chat connector |
| `POST /v1/audio/speech` | not_supported | Not part of standard SK OpenAI chat connector |
| `POST /v1/images/generations` | not_supported | Not default SK OpenAI connector path |
| `POST /v1/conversations/files` | gt_extension | Custom plugin HttpClient multipart upload |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom plugin HttpClient dataset upload |
| `GET /v1/files/{id}` | gt_extension | Custom plugin GET poll |

### Not supported in this product

- Semantic Kernel OpenAI connector does not expose GT multipart upload or conversation header semantics natively.

### Prerequisites

- Publish aliases for kernel prompts and planners.
- Include `inference:embed` when memory or RAG plugins call `/v1/embeddings`.

### Setup steps

1. Register OpenAI chat completion service with endpoint `${GT_BASE}` and GT bearer key.
2. Register embedding service to the same base when embed scope is on the key.
3. Use published alias as the model id in kernel prompts.
4. Validate one completion and one embedding batch before enabling autonomous plugins.

### GT extensions and caveats

- Author plugins that POST to `/v1/conversations` and attach `X-GT-Conversation-Id` on follow-ups.
- Use HttpClient in plugins for dataset or conversation file uploads and status polling.

### Validation checklist

- Kernel prompts complete with published aliases.
- Embedding calls succeed when embed scope is enabled.
- GT side effects are visible in application logs/telemetry.

### Plain-text export

```text
Semantic Kernel runbook
OpenAI plus GT extensions · Framework and orchestration
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Point Semantic Kernel OpenAI chat and embedding connectors at GT API; implement GT upload and conversation bootstrap in custom plugins or host services.

Official documentation:
- https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/chat-completion/
- https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.connectors.openai.openaichatcompletionservice
- https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/embedding-generation

Configuration fields:
- OpenAIChatCompletionService endpoint (C#): https://<tenant-host>/api/tenant
- ApiKey / OPENAI_API_KEY: gtak_...
- ModelId in kernel prompt: published-agent-alias

GT route mapping:
- GET /v1/models (native): ModelId must match published alias; validate with manual model list during setup
- POST /v1/chat/completions (native): OpenAIChatCompletionService → `/v1/chat/completions`
- POST /v1/embeddings (native): OpenAITextEmbeddingGenerationService → `/v1/embeddings`
- POST /v1/audio/transcriptions (not_supported): Not part of standard SK OpenAI chat connector
- POST /v1/audio/speech (not_supported): Not part of standard SK OpenAI chat connector
- POST /v1/images/generations (not_supported): Not default SK OpenAI connector path
- POST /v1/conversations/files (gt_extension): Custom plugin HttpClient multipart upload
- POST /v1/datasets/{id}/files (gt_extension): Custom plugin HttpClient dataset upload
- GET /v1/files/{id} (gt_extension): Custom plugin GET poll

Not supported in this product:
- Semantic Kernel OpenAI connector does not expose GT multipart upload or conversation header semantics natively.

Prerequisites:
- Publish aliases for kernel prompts and planners.
- Include `inference:embed` when memory or RAG plugins call `/v1/embeddings`.

Setup steps:
1. Register OpenAI chat completion service with endpoint `${GT_BASE}` and GT bearer key.
2. Register embedding service to the same base when embed scope is on the key.
3. Use published alias as the model id in kernel prompts.
4. Validate one completion and one embedding batch before enabling autonomous plugins.

GT extensions and caveats:
- Author plugins that POST to `/v1/conversations` and attach `X-GT-Conversation-Id` on follow-ups.
- Use HttpClient in plugins for dataset or conversation file uploads and status polling.

Validation checklist:
- Kernel prompts complete with published aliases.
- Embedding calls succeed when embed scope is enabled.
- GT side effects are visible in application logs/telemetry.
```
