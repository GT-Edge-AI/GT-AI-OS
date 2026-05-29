## Start Here

Use GT API as the OpenAI-compatible backend for Lovable-generated apps via server-side env configuration; keep GT conversation and upload routes in backend helpers, not browser bundles. Recommended preset: **Conversation app with uploads**.

## Why this matters

This runbook maps **Lovable** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Workflow and builders

### Official documentation

- https://docs.lovable.dev/
- https://docs.lovable.dev/features/environment-variables
- https://docs.lovable.dev/features/backend

### Configuration fields

- **GT_API_BASE_URL (server env):** `https://<tenant-host>/api/tenant`
- **GT_API_KEY (server env):** `gtak_...`
- **Model id in backend code:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Server fetch to `/v1/models` for app model picker |
| `POST /v1/chat/completions` | native | Server Route Handler → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | Server embedding helper when RAG needs `/v1/embeddings` |
| `POST /v1/audio/transcriptions` | not_supported | Not default Lovable template path |
| `POST /v1/audio/speech` | not_supported | Not default Lovable template path |
| `POST /v1/images/generations` | not_supported | Server call when image scope enabled on key |
| `POST /v1/conversations/files` | gt_extension | Server multipart POST to conversation files route |
| `POST /v1/datasets/{id}/files` | gt_extension | Server automation to dataset files route |
| `GET /v1/files/{id}` | gt_extension | Server GET poll on file id |

### Not supported in this product

- Lovable hosted builder may not support pointing all AI features at a custom OpenAI base URL without server-side backend code you control.
- Browser-exposed OpenAI keys cannot safely use GT bearer credentials.

### Prerequisites

- Publish alias the generated app should surface.
- Create linked inference + upload keys if using conversation-app preset.

### Setup steps

1. Add server env vars for GT base URL and API key in Lovable project settings.
2. Wire generated backend Route Handler to call GT `/v1/chat/completions` via OpenAI SDK or fetch.
3. Implement server helper for `POST /v1/conversations` and reuse id on follow-ups.
4. Never expose `gtak_...` in client-side JavaScript.

### GT extensions and caveats

- Use `/v1/conversations/files` from server routes tied to the same conversation id.
- Poll `/v1/files/{id}` server-side before attaching uploads to prompts.

### Validation checklist

- Generated app chats with GT alias.
- Conversation ids created server-side and reused correctly.
- GT API key stays within intended trust boundary.

### Plain-text export

```text
Lovable runbook
OpenAI plus GT extensions · Workflow and builders
Recommended key preset: Conversation app with uploads
Evidence: documented compatibility (vendor docs cross-check)

Use GT API as the OpenAI-compatible backend for Lovable-generated apps via server-side env configuration; keep GT conversation and upload routes in backend helpers, not browser bundles.

Official documentation:
- https://docs.lovable.dev/
- https://docs.lovable.dev/features/environment-variables
- https://docs.lovable.dev/features/backend

Configuration fields:
- GT_API_BASE_URL (server env): https://<tenant-host>/api/tenant
- GT_API_KEY (server env): gtak_...
- Model id in backend code: published-agent-alias

GT route mapping:
- GET /v1/models (native): Server fetch to `/v1/models` for app model picker
- POST /v1/chat/completions (native): Server Route Handler → `/v1/chat/completions`
- POST /v1/embeddings (native): Server embedding helper when RAG needs `/v1/embeddings`
- POST /v1/audio/transcriptions (not_supported): Not default Lovable template path
- POST /v1/audio/speech (not_supported): Not default Lovable template path
- POST /v1/images/generations (not_supported): Server call when image scope enabled on key
- POST /v1/conversations/files (gt_extension): Server multipart POST to conversation files route
- POST /v1/datasets/{id}/files (gt_extension): Server automation to dataset files route
- GET /v1/files/{id} (gt_extension): Server GET poll on file id

Not supported in this product:
- Lovable hosted builder may not support pointing all AI features at a custom OpenAI base URL without server-side backend code you control.
- Browser-exposed OpenAI keys cannot safely use GT bearer credentials.

Prerequisites:
- Publish alias the generated app should surface.
- Create linked inference + upload keys if using conversation-app preset.

Setup steps:
1. Add server env vars for GT base URL and API key in Lovable project settings.
2. Wire generated backend Route Handler to call GT `/v1/chat/completions` via OpenAI SDK or fetch.
3. Implement server helper for `POST /v1/conversations` and reuse id on follow-ups.
4. Never expose `gtak_...` in client-side JavaScript.

GT extensions and caveats:
- Use `/v1/conversations/files` from server routes tied to the same conversation id.
- Poll `/v1/files/{id}` server-side before attaching uploads to prompts.

Validation checklist:
- Generated app chats with GT alias.
- Conversation ids created server-side and reused correctly.
- GT API key stays within intended trust boundary.
```
