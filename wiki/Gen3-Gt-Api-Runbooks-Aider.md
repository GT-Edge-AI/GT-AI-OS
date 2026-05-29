## Start Here

Run Aider with `--openai-api-base` pointed at GT API and `OPENAI_API_KEY` set to a dedicated inference key; use a published coding alias as the model name. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Aider** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://aider.chat/docs/llms/openai.html
- https://aider.chat/docs/config/options.html
- https://aider.chat/docs/config/dotenv.html

### Configuration fields

- **--openai-api-base:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **--model:** `openai/published-coding-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | `--model` uses published alias string |
| `POST /v1/chat/completions` | native | Aider OpenAI client → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Not used in standard Aider workflow |
| `POST /v1/audio/transcriptions` | not_supported | Not supported |
| `POST /v1/audio/speech` | not_supported | Not supported |
| `POST /v1/images/generations` | not_supported | Not supported |
| `POST /v1/conversations/files` | not_supported | Not applicable |
| `POST /v1/datasets/{id}/files` | not_supported | Not applicable |
| `GET /v1/files/{id}` | not_supported | Not applicable |

### Not supported in this product

- Aider local file edits do not integrate with GT conversation or dataset upload APIs.

### Prerequisites

- Publish coding-oriented alias.
- Create dedicated chat-scoped inference key.

### Setup steps

1. Export `OPENAI_API_KEY=gtak_...` in shell or `.env`.
2. Run `aider --openai-api-base https://<tenant-host>/api/tenant --model openai/<published-alias>`.
3. Send a short prompt and confirm diff generation works.
4. Rotate key on schedule appropriate to CLI usage.

### GT extensions and caveats

- Standard Aider path does not use GT conversation uploads.
- Persisted GT conversations are usually unnecessary for CLI coding sessions.

### Validation checklist

- Aider completes a prompt with GT alias.
- Only intended alias exposed to that key.
- Works after key rotation.

### Plain-text export

```text
Aider runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Run Aider with `--openai-api-base` pointed at GT API and `OPENAI_API_KEY` set to a dedicated inference key; use a published coding alias as the model name.

Official documentation:
- https://aider.chat/docs/llms/openai.html
- https://aider.chat/docs/config/options.html
- https://aider.chat/docs/config/dotenv.html

Configuration fields:
- --openai-api-base: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- --model: openai/published-coding-alias

GT route mapping:
- GET /v1/models (native): `--model` uses published alias string
- POST /v1/chat/completions (native): Aider OpenAI client → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Not used in standard Aider workflow
- POST /v1/audio/transcriptions (not_supported): Not supported
- POST /v1/audio/speech (not_supported): Not supported
- POST /v1/images/generations (not_supported): Not supported
- POST /v1/conversations/files (not_supported): Not applicable
- POST /v1/datasets/{id}/files (not_supported): Not applicable
- GET /v1/files/{id} (not_supported): Not applicable

Not supported in this product:
- Aider local file edits do not integrate with GT conversation or dataset upload APIs.

Prerequisites:
- Publish coding-oriented alias.
- Create dedicated chat-scoped inference key.

Setup steps:
1. Export `OPENAI_API_KEY=gtak_...` in shell or `.env`.
2. Run `aider --openai-api-base https://<tenant-host>/api/tenant --model openai/<published-alias>`.
3. Send a short prompt and confirm diff generation works.
4. Rotate key on schedule appropriate to CLI usage.

GT extensions and caveats:
- Standard Aider path does not use GT conversation uploads.
- Persisted GT conversations are usually unnecessary for CLI coding sessions.

Validation checklist:
- Aider completes a prompt with GT alias.
- Only intended alias exposed to that key.
- Works after key rotation.
```
