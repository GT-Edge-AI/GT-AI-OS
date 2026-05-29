## Start Here

Add an OpenAI-compatible model provider in Continue config.yaml pointed at GT API with a dedicated editor-scoped inference key and published coding alias. Recommended preset: **Agentic IDE or editor client**.

## Why this matters

This runbook maps **Continue** to GT API routes operators actually publish.

## Details

**Compatibility:** Guided OpenAI-compatible setup · **Category:** Developer tooling

### Official documentation

- https://docs.continue.dev/customize/model-providers/openai
- https://docs.continue.dev/reference/json-reference
- https://docs.continue.dev/customize/model-providers/overview

### Configuration fields

- **config.yaml → models[].apiBase:** `https://<tenant-host>/api/tenant`
- **config.yaml → models[].apiKey:** `gtak_...`
- **config.yaml → models[].model:** `published-coding-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Model id in config must match published alias; optional manual `/v1/models` during setup |
| `POST /v1/chat/completions` | native | Continue OpenAI provider → `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Not used in standard Continue chat configuration |
| `POST /v1/audio/transcriptions` | not_supported | Not supported in Continue OpenAI chat path |
| `POST /v1/audio/speech` | not_supported | Not supported in Continue OpenAI chat path |
| `POST /v1/images/generations` | not_supported | Not supported in Continue OpenAI chat path |
| `POST /v1/conversations/files` | not_supported | Not applicable to editor chat workflow |
| `POST /v1/datasets/{id}/files` | not_supported | Not applicable to editor chat workflow |
| `GET /v1/files/{id}` | not_supported | Not applicable to editor chat workflow |

### Not supported in this product

- Continue does not expose GT dataset or conversation upload workflows in standard editor chat.

### Prerequisites

- Publish at least one coding-oriented agent alias.
- Create dedicated agentic-editor inference key.

### Setup steps

1. Edit Continue config → add model block with `apiBase: https://<tenant-host>/api/tenant`.
2. Set `apiKey` to GT bearer token (Continue secret storage or env reference).
3. Set `model` field to published alias from `GET /v1/models`.
4. Open Continue chat panel and send a short coding prompt to validate.

### GT extensions and caveats

- Continue coding flow does not require GT conversation uploads.
- Treat MCP and other Continue tools as separate from GT API compatibility.

### Validation checklist

- Continue lists or targets the GT alias successfully.
- Responses stable after key rotation.
- Key is narrow — no unexpected aliases visible.

### Plain-text export

```text
Continue runbook
Guided OpenAI-compatible setup · Developer tooling
Recommended key preset: Agentic IDE or editor client
Evidence: documented compatibility (vendor docs cross-check)

Add an OpenAI-compatible model provider in Continue config.yaml pointed at GT API with a dedicated editor-scoped inference key and published coding alias.

Official documentation:
- https://docs.continue.dev/customize/model-providers/openai
- https://docs.continue.dev/reference/json-reference
- https://docs.continue.dev/customize/model-providers/overview

Configuration fields:
- config.yaml → models[].apiBase: https://<tenant-host>/api/tenant
- config.yaml → models[].apiKey: gtak_...
- config.yaml → models[].model: published-coding-alias

GT route mapping:
- GET /v1/models (native): Model id in config must match published alias; optional manual `/v1/models` during setup
- POST /v1/chat/completions (native): Continue OpenAI provider → `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Not used in standard Continue chat configuration
- POST /v1/audio/transcriptions (not_supported): Not supported in Continue OpenAI chat path
- POST /v1/audio/speech (not_supported): Not supported in Continue OpenAI chat path
- POST /v1/images/generations (not_supported): Not supported in Continue OpenAI chat path
- POST /v1/conversations/files (not_supported): Not applicable to editor chat workflow
- POST /v1/datasets/{id}/files (not_supported): Not applicable to editor chat workflow
- GET /v1/files/{id} (not_supported): Not applicable to editor chat workflow

Not supported in this product:
- Continue does not expose GT dataset or conversation upload workflows in standard editor chat.

Prerequisites:
- Publish at least one coding-oriented agent alias.
- Create dedicated agentic-editor inference key.

Setup steps:
1. Edit Continue config → add model block with `apiBase: https://<tenant-host>/api/tenant`.
2. Set `apiKey` to GT bearer token (Continue secret storage or env reference).
3. Set `model` field to published alias from `GET /v1/models`.
4. Open Continue chat panel and send a short coding prompt to validate.

GT extensions and caveats:
- Continue coding flow does not require GT conversation uploads.
- Treat MCP and other Continue tools as separate from GT API compatibility.

Validation checklist:
- Continue lists or targets the GT alias successfully.
- Responses stable after key rotation.
- Key is narrow — no unexpected aliases visible.
```
