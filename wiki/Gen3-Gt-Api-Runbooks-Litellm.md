## Start Here

Point LiteLLM at GT API as an OpenAI-compatible upstream for chat and embeddings; keep GT upload and conversation routes in adjacent services. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **LiteLLM** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** Framework and orchestration

### Official documentation

- https://docs.litellm.ai/docs/providers/openai
- https://docs.litellm.ai/docs/proxy/configs
- https://docs.litellm.ai/docs/embedding/supported_embedding

### Configuration fields

- **litellm_settings.api_base (proxy):** `https://<tenant-host>/api/tenant`
- **model_list[].litellm_params.api_base:** `https://<tenant-host>/api/tenant`
- **model_list[].litellm_params.api_key:** `gtak_...`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Proxy may passthrough `GET /v1/models` or use static alias map — validate explicitly |
| `POST /v1/chat/completions` | native | LiteLLM `completion()` forwards to GT `/v1/chat/completions` |
| `POST /v1/embeddings` | native | LiteLLM `embedding()` forwards to GT `/v1/embeddings` when configured |
| `POST /v1/audio/transcriptions` | not_supported | Not a default LiteLLM OpenAI proxy path for GT |
| `POST /v1/audio/speech` | not_supported | Not a default LiteLLM OpenAI proxy path for GT |
| `POST /v1/images/generations` | not_supported | Requires explicit image route configuration and GT image scope |
| `POST /v1/conversations/files` | gt_extension | External HTTP job — not LiteLLM core router |
| `POST /v1/datasets/{id}/files` | gt_extension | External HTTP job — not LiteLLM core router |
| `GET /v1/files/{id}` | gt_extension | External polling script |

### Not supported in this product

- LiteLLM does not natively expose GT conversation headers or dataset upload multipart semantics.

### Prerequisites

- Prove GT API with curl or OpenAI SDK first.
- Create narrowly scoped inference key including `inference:embed` only when downstream apps need embeddings.

### Setup steps

1. Configure GT as OpenAI-compatible upstream in LiteLLM proxy or pass `api_base` per request.
2. Map published GT aliases as LiteLLM model names exposed to downstream consumers.
3. Enable embedding route tests with `litellm.embedding()` when embed scope is on the key.
4. Verify one non-streaming chat completion through LiteLLM before broader rollout.

### GT extensions and caveats

- Do not expect LiteLLM router to translate GT multipart upload or conversation bootstrap automatically.
- Run GT-specific HTTP from automation outside the proxy when uploads are required.

### Validation checklist

- Downstream clients see expected alias list or static model map.
- Chat and embedding responses remain OpenAI-shaped through the proxy.
- Rotating the upstream GT key does not require downstream model id changes.

### Plain-text export

```text
LiteLLM runbook
Native OpenAI-compatible · Framework and orchestration
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Point LiteLLM at GT API as an OpenAI-compatible upstream for chat and embeddings; keep GT upload and conversation routes in adjacent services.

Official documentation:
- https://docs.litellm.ai/docs/providers/openai
- https://docs.litellm.ai/docs/proxy/configs
- https://docs.litellm.ai/docs/embedding/supported_embedding

Configuration fields:
- litellm_settings.api_base (proxy): https://<tenant-host>/api/tenant
- model_list[].litellm_params.api_base: https://<tenant-host>/api/tenant
- model_list[].litellm_params.api_key: gtak_...

GT route mapping:
- GET /v1/models (native): Proxy may passthrough `GET /v1/models` or use static alias map — validate explicitly
- POST /v1/chat/completions (native): LiteLLM `completion()` forwards to GT `/v1/chat/completions`
- POST /v1/embeddings (native): LiteLLM `embedding()` forwards to GT `/v1/embeddings` when configured
- POST /v1/audio/transcriptions (not_supported): Not a default LiteLLM OpenAI proxy path for GT
- POST /v1/audio/speech (not_supported): Not a default LiteLLM OpenAI proxy path for GT
- POST /v1/images/generations (not_supported): Requires explicit image route configuration and GT image scope
- POST /v1/conversations/files (gt_extension): External HTTP job — not LiteLLM core router
- POST /v1/datasets/{id}/files (gt_extension): External HTTP job — not LiteLLM core router
- GET /v1/files/{id} (gt_extension): External polling script

Not supported in this product:
- LiteLLM does not natively expose GT conversation headers or dataset upload multipart semantics.

Prerequisites:
- Prove GT API with curl or OpenAI SDK first.
- Create narrowly scoped inference key including `inference:embed` only when downstream apps need embeddings.

Setup steps:
1. Configure GT as OpenAI-compatible upstream in LiteLLM proxy or pass `api_base` per request.
2. Map published GT aliases as LiteLLM model names exposed to downstream consumers.
3. Enable embedding route tests with `litellm.embedding()` when embed scope is on the key.
4. Verify one non-streaming chat completion through LiteLLM before broader rollout.

GT extensions and caveats:
- Do not expect LiteLLM router to translate GT multipart upload or conversation bootstrap automatically.
- Run GT-specific HTTP from automation outside the proxy when uploads are required.

Validation checklist:
- Downstream clients see expected alias list or static model map.
- Chat and embedding responses remain OpenAI-shaped through the proxy.
- Rotating the upstream GT key does not require downstream model id changes.
```
