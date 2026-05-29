## Start Here

Point Hermes Agent at the tenant GT API with a first-class custom OpenAI-compatible endpoint (`provider: custom`, `base_url`, `api_key`); use a published agent alias as the model id after validating `GET /v1/models`. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Hermes Agent** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** Developer tooling

### Official documentation

- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/developer-guide/adding-providers
- https://github.com/NousResearch/hermes-agent

### Configuration fields

- **model.provider:** `custom`
- **model.base_url:** `https://<tenant-host>/api/tenant`
- **model.api_key:** `gtak_...`
- **model.default (or model.model):** `published-agent-alias`
- **custom_providers[].api_mode:** `chat_completions`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Set `model.default` to published alias; optional `GET /v1/models` during setup |
| `POST /v1/chat/completions` | native | Hermes custom provider (`api_mode: chat_completions`) → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Only if you add explicit embed calls in agent tooling |
| `POST /v1/audio/transcriptions` | not_supported | Not default Hermes OpenAI custom path |
| `POST /v1/audio/speech` | not_supported | Not default Hermes OpenAI custom path |
| `POST /v1/images/generations` | not_supported | Not default unless auxiliary vision routes to GT |
| `POST /v1/conversations/files` | gt_extension | Custom HTTP orchestration outside Hermes defaults |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom HTTP orchestration outside Hermes defaults |
| `GET /v1/files/{id}` | gt_extension | Custom polling in agent tooling |

### Not supported in this product

- Hermes auxiliary/vision routing may target a different provider unless you configure every task to use the GT custom endpoint.
- Hermes does not manage GT conversation headers or dataset multipart uploads in the default custom-provider path.

### Prerequisites

- Hermes Agent installed (`hermes setup` or package install per Nous Research docs).
- Publish at least one agent alias or raw-model catalog entry for agentic chat.
- Create a dedicated agentic-editor inference key scoped to intended aliases.

### Setup steps

1. Run `hermes model` and choose **Custom endpoint**, or edit `~/.hermes/config.yaml`.
2. Set base URL to https://<tenant-host>/api/tenant (Hermes appends /v1/chat/completions — do not include a trailing /v1 segment unless your Hermes build expects the full path; use the tenant origin ending in /api/tenant).
3. Set API key to a GT bearer token (`gtak_...`).
4. Set the model name to a published alias from `GET /v1/models`.
5. Send a short prompt in the Hermes terminal UI and confirm the response uses the GT-published model.

### GT extensions and caveats

- Hermes does not natively send `X-GT-Conversation-Id` or multipart dataset uploads — add explicit HTTP only if you orchestrate GT file routes yourself.
- Agent runners can generate sustained traffic; monitor quotas and keep alias allowlists narrow on the inference key.

### Validation checklist

- Hermes custom provider reaches GT API without 401/404 on chat.
- Model id matches a published alias visible to that key.
- Revoking or rotating the GT key stops Hermes traffic as expected.

### Plain-text export

```text
Hermes Agent runbook
Native OpenAI-compatible · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Point Hermes Agent at the tenant GT API with a first-class custom OpenAI-compatible endpoint (`provider: custom`, `base_url`, `api_key`); use a published agent alias as the model id after validating `GET /v1/models`.

Official documentation:
- https://hermes-agent.nousresearch.com/docs/integrations/providers
- https://hermes-agent.nousresearch.com/docs/developer-guide/adding-providers
- https://github.com/NousResearch/hermes-agent

Configuration fields:
- model.provider: custom
- model.base_url: https://<tenant-host>/api/tenant
- model.api_key: gtak_...
- model.default (or model.model): published-agent-alias
- custom_providers[].api_mode: chat_completions

GT route mapping:
- GET /v1/models (native): Set `model.default` to published alias; optional `GET /v1/models` during setup
- POST /v1/chat/completions (native): Hermes custom provider (`api_mode: chat_completions`) → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Only if you add explicit embed calls in agent tooling
- POST /v1/audio/transcriptions (not_supported): Not default Hermes OpenAI custom path
- POST /v1/audio/speech (not_supported): Not default Hermes OpenAI custom path
- POST /v1/images/generations (not_supported): Not default unless auxiliary vision routes to GT
- POST /v1/conversations/files (gt_extension): Custom HTTP orchestration outside Hermes defaults
- POST /v1/datasets/{id}/files (gt_extension): Custom HTTP orchestration outside Hermes defaults
- GET /v1/files/{id} (gt_extension): Custom polling in agent tooling

Not supported in this product:
- Hermes auxiliary/vision routing may target a different provider unless you configure every task to use the GT custom endpoint.
- Hermes does not manage GT conversation headers or dataset multipart uploads in the default custom-provider path.

Prerequisites:
- Hermes Agent installed (`hermes setup` or package install per Nous Research docs).
- Publish at least one agent alias or raw-model catalog entry for agentic chat.
- Create a dedicated agentic-editor inference key scoped to intended aliases.

Setup steps:
1. Run `hermes model` and choose **Custom endpoint**, or edit `~/.hermes/config.yaml`.
2. Set base URL to https://<tenant-host>/api/tenant (Hermes appends /v1/chat/completions — do not include a trailing /v1 segment unless your Hermes build expects the full path; use the tenant origin ending in /api/tenant).
3. Set API key to a GT bearer token (`gtak_...`).
4. Set the model name to a published alias from `GET /v1/models`.
5. Send a short prompt in the Hermes terminal UI and confirm the response uses the GT-published model.

GT extensions and caveats:
- Hermes does not natively send `X-GT-Conversation-Id` or multipart dataset uploads — add explicit HTTP only if you orchestrate GT file routes yourself.
- Agent runners can generate sustained traffic; monitor quotas and keep alias allowlists narrow on the inference key.

Validation checklist:
- Hermes custom provider reaches GT API without 401/404 on chat.
- Model id matches a published alias visible to that key.
- Revoking or rotating the GT key stops Hermes traffic as expected.
```
