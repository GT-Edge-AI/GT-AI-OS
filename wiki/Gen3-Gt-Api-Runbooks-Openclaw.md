## Start Here

Configure OpenClaw (or compatible agent runners) with OpenAI-compatible base URL and bearer key when the runtime supports custom endpoints; validate model discovery before autonomous modes. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **OpenClaw** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://github.com/openclaw/openclaw
- https://docs.openclaw.ai/
- https://github.com/openclaw/openclaw/blob/main/README.md

### Configuration fields

- **OPENAI_BASE_URL / openai_base_url:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **Agent model / default_model:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Agent startup should call or assume published alias from `GET /v1/models` |
| `POST /v1/chat/completions` | native | Agent OpenAI client → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Only if agent config explicitly calls embed route |
| `POST /v1/audio/transcriptions` | not_supported | Not default OpenClaw OpenAI integration |
| `POST /v1/audio/speech` | not_supported | Not default OpenClaw OpenAI integration |
| `POST /v1/images/generations` | not_supported | Not default unless agent adds image route calls |
| `POST /v1/conversations/files` | gt_extension | Custom HTTP orchestration in agent tooling |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom HTTP orchestration in agent tooling |
| `GET /v1/files/{id}` | gt_extension | Custom polling in agent tooling |

### Not supported in this product

- OpenClaw does not natively manage GT conversation headers or multipart dataset uploads.

### Prerequisites

- Confirm runtime supports custom OpenAI-compatible endpoints.
- Create dedicated inference key scoped to intended aliases.

### Setup steps

1. Set API base URL to tenant GT API origin ending in `/api/tenant`.
2. Configure bearer authentication with GT API key.
3. Validate `GET /v1/models` and one minimal chat completion.
4. Enable higher autonomy only after base path is stable.

### GT extensions and caveats

- Add GT conversation/upload HTTP only through orchestration you control.
- Treat traffic bursts as normal for agent runners.

### Validation checklist

- Model discovery matches key allowlist.
- Completions succeed with intended published alias.
- Revoking key stops agent traffic without side effects.

### Plain-text export

```text
OpenClaw runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Configure OpenClaw (or compatible agent runners) with OpenAI-compatible base URL and bearer key when the runtime supports custom endpoints; validate model discovery before autonomous modes.

Official documentation:
- https://github.com/openclaw/openclaw
- https://docs.openclaw.ai/
- https://github.com/openclaw/openclaw/blob/main/README.md

Configuration fields:
- OPENAI_BASE_URL / openai_base_url: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- Agent model / default_model: published-agent-alias

GT route mapping:
- GET /v1/models (native): Agent startup should call or assume published alias from `GET /v1/models`
- POST /v1/chat/completions (native): Agent OpenAI client → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Only if agent config explicitly calls embed route
- POST /v1/audio/transcriptions (not_supported): Not default OpenClaw OpenAI integration
- POST /v1/audio/speech (not_supported): Not default OpenClaw OpenAI integration
- POST /v1/images/generations (not_supported): Not default unless agent adds image route calls
- POST /v1/conversations/files (gt_extension): Custom HTTP orchestration in agent tooling
- POST /v1/datasets/{id}/files (gt_extension): Custom HTTP orchestration in agent tooling
- GET /v1/files/{id} (gt_extension): Custom polling in agent tooling

Not supported in this product:
- OpenClaw does not natively manage GT conversation headers or multipart dataset uploads.

Prerequisites:
- Confirm runtime supports custom OpenAI-compatible endpoints.
- Create dedicated inference key scoped to intended aliases.

Setup steps:
1. Set API base URL to tenant GT API origin ending in `/api/tenant`.
2. Configure bearer authentication with GT API key.
3. Validate `GET /v1/models` and one minimal chat completion.
4. Enable higher autonomy only after base path is stable.

GT extensions and caveats:
- Add GT conversation/upload HTTP only through orchestration you control.
- Treat traffic bursts as normal for agent runners.

Validation checklist:
- Model discovery matches key allowlist.
- Completions succeed with intended published alias.
- Revoking key stops agent traffic without side effects.
```
