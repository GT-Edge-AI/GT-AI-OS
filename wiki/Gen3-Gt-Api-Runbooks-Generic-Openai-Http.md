## Start Here

Fallback row for unlisted products that can override OpenAI base URL and send bearer-authenticated requests to `/api/tenant/v1/*`. Recommended preset: **OpenAI-compatible chat client**.

## Why this matters

This runbook maps **Generic OpenAI-compatible HTTP client** to GT API routes operators actually publish.

## Details

**Compatibility:** Native OpenAI-compatible · **Category:** SDK and HTTP

### Official documentation

- https://platform.openai.com/docs/api-reference/introduction
- https://swagger.io/docs/specification/authentication/bearer-authentication/
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization

### Configuration fields

- **Base URL / api_base / OPENAI_BASE_URL:** `https://<tenant-host>/api/tenant`
- **Authorization: Bearer:** `gtak_...`
- **model (request body):** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Client HTTP GET `/v1/models` or static alias configuration |
| `POST /v1/chat/completions` | native | Client HTTP POST `/v1/chat/completions` with JSON body |
| `POST /v1/embeddings` | native | Client HTTP POST `/v1/embeddings` when key includes embed scope |
| `POST /v1/audio/transcriptions` | native | Client HTTP multipart POST `/v1/audio/transcriptions` when transcribe scope enabled |
| `POST /v1/audio/speech` | native | Client HTTP POST `/v1/audio/speech` when speech scope enabled |
| `POST /v1/images/generations` | native | Client HTTP POST `/v1/images/generations` when image scope enabled |
| `POST /v1/conversations/files` | gt_extension | Client HTTP multipart POST `/v1/conversations/files` with GT headers |
| `POST /v1/datasets/{id}/files` | gt_extension | Client HTTP multipart POST `/v1/datasets/{id}/files` |
| `GET /v1/files/{id}` | gt_extension | Client HTTP GET `/v1/files/{id}` polling |

### Not supported in this product

- Products that only speak vendor-native APIs and cannot set a custom OpenAI-compatible URL are not direct GT API clients.

### Prerequisites

- Create narrowest key preset matching actual client behavior.
- Confirm client can override both base URL and bearer auth.

### Setup steps

1. Configure base URL to tenant GT API origin ending in `/api/tenant`.
2. Set bearer token to GT API key from key creation.
3. Validate model discovery and one chat completion.
4. Add GT conversation/upload routes only if required by the integration.

### GT extensions and caveats

- Layer `POST /v1/conversations`, upload routes, and file polling beside standard chat when needed.
- Use this row when the product is unlisted but meets the custom OpenAI URL criteria.

### Validation checklist

- Client can list models and complete chat with published alias.
- Optional GT routes work when explicitly implemented.
- Key scope matches actual routes exercised.

### Plain-text export

```text
Generic OpenAI-compatible HTTP client runbook
Native OpenAI-compatible · SDK and HTTP
Recommended key preset: OpenAI-compatible chat client
Evidence: documented compatibility (vendor docs cross-check)

Fallback row for unlisted products that can override OpenAI base URL and send bearer-authenticated requests to `/api/tenant/v1/*`.

Official documentation:
- https://platform.openai.com/docs/api-reference/introduction
- https://swagger.io/docs/specification/authentication/bearer-authentication/
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization

Configuration fields:
- Base URL / api_base / OPENAI_BASE_URL: https://<tenant-host>/api/tenant
- Authorization: Bearer: gtak_...
- model (request body): published-agent-alias

GT route mapping:
- GET /v1/models (native): Client HTTP GET `/v1/models` or static alias configuration
- POST /v1/chat/completions (native): Client HTTP POST `/v1/chat/completions` with JSON body
- POST /v1/embeddings (native): Client HTTP POST `/v1/embeddings` when key includes embed scope
- POST /v1/audio/transcriptions (native): Client HTTP multipart POST `/v1/audio/transcriptions` when transcribe scope enabled
- POST /v1/audio/speech (native): Client HTTP POST `/v1/audio/speech` when speech scope enabled
- POST /v1/images/generations (native): Client HTTP POST `/v1/images/generations` when image scope enabled
- POST /v1/conversations/files (gt_extension): Client HTTP multipart POST `/v1/conversations/files` with GT headers
- POST /v1/datasets/{id}/files (gt_extension): Client HTTP multipart POST `/v1/datasets/{id}/files`
- GET /v1/files/{id} (gt_extension): Client HTTP GET `/v1/files/{id}` polling

Not supported in this product:
- Products that only speak vendor-native APIs and cannot set a custom OpenAI-compatible URL are not direct GT API clients.

Prerequisites:
- Create narrowest key preset matching actual client behavior.
- Confirm client can override both base URL and bearer auth.

Setup steps:
1. Configure base URL to tenant GT API origin ending in `/api/tenant`.
2. Set bearer token to GT API key from key creation.
3. Validate model discovery and one chat completion.
4. Add GT conversation/upload routes only if required by the integration.

GT extensions and caveats:
- Layer `POST /v1/conversations`, upload routes, and file polling beside standard chat when needed.
- Use this row when the product is unlisted but meets the custom OpenAI URL criteria.

Validation checklist:
- Client can list models and complete chat with published alias.
- Optional GT routes work when explicitly implemented.
- Key scope matches actual routes exercised.
```
