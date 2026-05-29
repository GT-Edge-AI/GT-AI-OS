## Start Here

Manus is primarily a hosted agent product; GT API fits only when your deployment exposes a true OpenAI-compatible base URL override — not the default Manus Custom API shape alone. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Manus** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://manus.im/docs
- https://manus.im/help
- https://open.manus.ai/docs

### Configuration fields

- **Custom API / OpenAI Base URL (when available):** `https://<tenant-host>/api/tenant`
- **API Key:** `gtak_...`
- **Model name:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Only when Manus accepts custom OpenAI base — alias must match published name |
| `POST /v1/chat/completions` | native | Manus task chat → `/v1/chat/completions` when OpenAI-compatible override works |
| `POST /v1/embeddings` | not_supported | Not documented as standard Manus custom API path |
| `POST /v1/audio/transcriptions` | not_supported | Not supported via Manus custom API |
| `POST /v1/audio/speech` | not_supported | Not supported via Manus custom API |
| `POST /v1/images/generations` | not_supported | Not supported via Manus custom API |
| `POST /v1/conversations/files` | not_supported | Requires custom orchestration outside Manus defaults |
| `POST /v1/datasets/{id}/files` | not_supported | Requires custom orchestration outside Manus defaults |
| `GET /v1/files/{id}` | not_supported | Requires custom orchestration outside Manus defaults |

### Not supported in this product

- Manus Custom API defaults are not a standard OpenAI `/v1` base URL — GT API requires explicit OpenAI-compatible override support.
- Hosted Manus SaaS without custom base URL cannot target GT API directly.

### Prerequisites

- Confirm your Manus tier allows arbitrary OpenAI-compatible base URLs (not just hosted Manus models).
- Create dedicated agentic-editor inference key.

### Setup steps

1. Open Manus provider/API settings and locate OpenAI-compatible or Custom API configuration.
2. If base URL override is available, set `https://<tenant-host>/api/tenant` and GT API key.
3. Map model name to published alias; run one short task.
4. Stop rollout if Manus requires Manus-hosted endpoints only.

### GT extensions and caveats

- Add wrapper HTTP only after chat-only path is stable.
- Do not over-scope keys until base URL compatibility is proven.

### Validation checklist

- First completion succeeds with GT alias when override works.
- Uses dedicated key.
- Revocation/rotation is operationally straightforward.

### Plain-text export

```text
Manus runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Manus is primarily a hosted agent product; GT API fits only when your deployment exposes a true OpenAI-compatible base URL override — not the default Manus Custom API shape alone.

Official documentation:
- https://manus.im/docs
- https://manus.im/help
- https://open.manus.ai/docs

Configuration fields:
- Custom API / OpenAI Base URL (when available): https://<tenant-host>/api/tenant
- API Key: gtak_...
- Model name: published-agent-alias

GT route mapping:
- GET /v1/models (native): Only when Manus accepts custom OpenAI base — alias must match published name
- POST /v1/chat/completions (native): Manus task chat → `/v1/chat/completions` when OpenAI-compatible override works
- POST /v1/embeddings (not_supported): Not documented as standard Manus custom API path
- POST /v1/audio/transcriptions (not_supported): Not supported via Manus custom API
- POST /v1/audio/speech (not_supported): Not supported via Manus custom API
- POST /v1/images/generations (not_supported): Not supported via Manus custom API
- POST /v1/conversations/files (not_supported): Requires custom orchestration outside Manus defaults
- POST /v1/datasets/{id}/files (not_supported): Requires custom orchestration outside Manus defaults
- GET /v1/files/{id} (not_supported): Requires custom orchestration outside Manus defaults

Not supported in this product:
- Manus Custom API defaults are not a standard OpenAI `/v1` base URL — GT API requires explicit OpenAI-compatible override support.
- Hosted Manus SaaS without custom base URL cannot target GT API directly.

Prerequisites:
- Confirm your Manus tier allows arbitrary OpenAI-compatible base URLs (not just hosted Manus models).
- Create dedicated agentic-editor inference key.

Setup steps:
1. Open Manus provider/API settings and locate OpenAI-compatible or Custom API configuration.
2. If base URL override is available, set `https://<tenant-host>/api/tenant` and GT API key.
3. Map model name to published alias; run one short task.
4. Stop rollout if Manus requires Manus-hosted endpoints only.

GT extensions and caveats:
- Add wrapper HTTP only after chat-only path is stable.
- Do not over-scope keys until base URL compatibility is proven.

Validation checklist:
- First completion succeeds with GT alias when override works.
- Uses dedicated key.
- Revocation/rotation is operationally straightforward.
```
