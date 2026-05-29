## Start Here

Configure AnythingLLM Generic OpenAI LLM connection with the GT API base URL and key; align chat and optional embedding calls with the same published alias boundary. Recommended preset: **Chat plus embeddings framework client**.

## Why this matters

This runbook maps **AnythingLLM** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Workflow and builders

### Official documentation

- https://docs.anythingllm.com/setup/llm-configuration/custom/openai
- https://docs.anythingllm.com/features/chat-ui
- https://docs.anythingllm.com/setup/embedder-configuration/local

### Configuration fields

- **Generic OpenAI → API Base URL:** `https://<tenant-host>/api/tenant`
- **Generic OpenAI → API Key:** `gtak_...`
- **Generic OpenAI → Model:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Model field set to published alias; optional admin test calls `/v1/models` |
| `POST /v1/chat/completions` | native | AnythingLLM Generic OpenAI chat → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | Generic OpenAI embedder pointed at GT when embed scope enabled |
| `POST /v1/audio/transcriptions` | not_supported | Not part of AnythingLLM Generic OpenAI chat setup |
| `POST /v1/audio/speech` | not_supported | Not part of AnythingLLM Generic OpenAI chat setup |
| `POST /v1/images/generations` | not_supported | Not supported in standard AnythingLLM OpenAI chat configuration |
| `POST /v1/conversations/files` | not_supported | External automation — not default workspace upload path |
| `POST /v1/datasets/{id}/files` | not_supported | External automation to GT dataset upload route |
| `GET /v1/files/{id}` | not_supported | External polling after GT upload |

### Not supported in this product

- AnythingLLM workspace document pipeline does not natively upload to GT dataset routes.
- Default embedder may bypass GT unless explicitly configured to use Generic OpenAI against GT base.

### Prerequisites

- Decide whether embeddings run through GT or AnythingLLM-local models.
- Create inference key with chat-only or chat+embed scopes accordingly.

### Setup steps

1. Open AnythingLLM admin → LLM Preference → Generic OpenAI.
2. Set API Base URL to `https://<tenant-host>/api/tenant` and paste GT API key.
3. Enter published alias as the chat model name.
4. Run a short workspace chat test before broader rollout.

### GT extensions and caveats

- AnythingLLM document uploads do not replace GT dataset ingestion — add external scripts if needed.
- Integrate GT conversations outside the default LLM connector when persisted GT threads are required.

### Validation checklist

- Workspace chat completes with the GT alias.
- Embedding traffic through GT succeeds when embed scope is enabled.
- Operators understand published alias vs UI display labels.

### Plain-text export

```text
AnythingLLM runbook
Guided OpenAI-compatible setup · Workflow and builders
Recommended key preset: Chat plus embeddings framework client
Evidence: documented compatibility (vendor docs cross-check)

Configure AnythingLLM Generic OpenAI LLM connection with the GT API base URL and key; align chat and optional embedding calls with the same published alias boundary.

Official documentation:
- https://docs.anythingllm.com/setup/llm-configuration/custom/openai
- https://docs.anythingllm.com/features/chat-ui
- https://docs.anythingllm.com/setup/embedder-configuration/local

Configuration fields:
- Generic OpenAI → API Base URL: https://<tenant-host>/api/tenant
- Generic OpenAI → API Key: gtak_...
- Generic OpenAI → Model: published-agent-alias

GT route mapping:
- GET /v1/models (native): Model field set to published alias; optional admin test calls `/v1/models`
- POST /v1/chat/completions (native): AnythingLLM Generic OpenAI chat → `/v1/chat/completions`
- POST /v1/embeddings (native): Generic OpenAI embedder pointed at GT when embed scope enabled
- POST /v1/audio/transcriptions (not_supported): Not part of AnythingLLM Generic OpenAI chat setup
- POST /v1/audio/speech (not_supported): Not part of AnythingLLM Generic OpenAI chat setup
- POST /v1/images/generations (not_supported): Not supported in standard AnythingLLM OpenAI chat configuration
- POST /v1/conversations/files (not_supported): External automation — not default workspace upload path
- POST /v1/datasets/{id}/files (not_supported): External automation to GT dataset upload route
- GET /v1/files/{id} (not_supported): External polling after GT upload

Not supported in this product:
- AnythingLLM workspace document pipeline does not natively upload to GT dataset routes.
- Default embedder may bypass GT unless explicitly configured to use Generic OpenAI against GT base.

Prerequisites:
- Decide whether embeddings run through GT or AnythingLLM-local models.
- Create inference key with chat-only or chat+embed scopes accordingly.

Setup steps:
1. Open AnythingLLM admin → LLM Preference → Generic OpenAI.
2. Set API Base URL to `https://<tenant-host>/api/tenant` and paste GT API key.
3. Enter published alias as the chat model name.
4. Run a short workspace chat test before broader rollout.

GT extensions and caveats:
- AnythingLLM document uploads do not replace GT dataset ingestion — add external scripts if needed.
- Integrate GT conversations outside the default LLM connector when persisted GT threads are required.

Validation checklist:
- Workspace chat completes with the GT alias.
- Embedding traffic through GT succeeds when embed scope is enabled.
- Operators understand published alias vs UI display labels.
```
