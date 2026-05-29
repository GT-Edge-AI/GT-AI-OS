## Start Here

Use the Vercel AI SDK OpenAI provider pointed at GT API for chat; implement GT conversation bootstrap and file uploads in Next.js route handlers or server actions. Recommended preset: **Conversation app with uploads**.

## Why this matters

This runbook maps **Vercel AI SDK** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Framework and orchestration

### Official documentation

- https://sdk.vercel.ai/docs/providers/openai
- https://sdk.vercel.ai/docs/ai-sdk-core/generating-text
- https://sdk.vercel.ai/docs/ai-sdk-core/settings

### Configuration fields

- **GT_API_BASE_URL (server env):** `https://<tenant-host>/api/tenant`
- **GT_API_KEY (server env):** `gtak_...`
- **createOpenAI({ baseURL, apiKey }):** `server-only instantiation`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Optional server fetch to `/v1/models` to populate UI model picker |
| `POST /v1/chat/completions` | native | `streamText` / `generateText` with OpenAI provider → `/v1/chat/completions` |
| `POST /v1/embeddings` | native | `embed` helper with OpenAI provider when RAG routes need `/v1/embeddings` |
| `POST /v1/audio/transcriptions` | not_supported | Not covered by default AI SDK OpenAI chat provider |
| `POST /v1/audio/speech` | not_supported | Not covered by default AI SDK OpenAI chat provider |
| `POST /v1/images/generations` | not_supported | Use experimental image helpers only with image-scoped GT keys |
| `POST /v1/conversations/files` | gt_extension | Server Route Handler multipart to `/v1/conversations/files` |
| `POST /v1/datasets/{id}/files` | gt_extension | Server automation to `/v1/datasets/{id}/files` when needed |
| `GET /v1/files/{id}` | gt_extension | Server polling `GET /v1/files/{id}` |

### Not supported in this product

- Vercel AI SDK Responses API (`openai.responses`) is not the GT-validated chat surface — use Chat Completions provider methods.
- Client Components cannot safely hold GT bearer keys; keep all GT calls server-side.

### Prerequisites

- Publish the alias the UI should display as its model name.
- Create conversation-app key (linked inference + upload keys) when chat and files share one external credential.

### Setup steps

1. Add server-only env `GT_API_BASE_URL=${GT_BASE}` and `GT_API_KEY=gtak_...`.
2. Instantiate `createOpenAI({ baseURL: process.env.GT_API_BASE_URL, apiKey: process.env.GT_API_KEY })`.
3. Call `streamText({ model: openai('<published-alias>'), messages })` from a Route Handler.
4. On thread start, `POST /v1/conversations` server-side and attach returned id to subsequent requests.

### GT extensions and caveats

- Upload attachments with `POST /v1/conversations/files` and the same conversation header from server code.
- Poll `GET /v1/files/{id}` before attaching file content to model context.

### Validation checklist

- Client receives streamed tokens without leaking the GT API key.
- Follow-up turns reuse the same GT conversation id.
- File upload + ready polling works for conversation-scoped attachments.

### Plain-text export

```text
Vercel AI SDK runbook
OpenAI plus GT extensions · Framework and orchestration
Recommended key preset: Conversation app with uploads
Evidence: documented compatibility (vendor docs cross-check)

Use the Vercel AI SDK OpenAI provider pointed at GT API for chat; implement GT conversation bootstrap and file uploads in Next.js route handlers or server actions.

Official documentation:
- https://sdk.vercel.ai/docs/providers/openai
- https://sdk.vercel.ai/docs/ai-sdk-core/generating-text
- https://sdk.vercel.ai/docs/ai-sdk-core/settings

Configuration fields:
- GT_API_BASE_URL (server env): https://<tenant-host>/api/tenant
- GT_API_KEY (server env): gtak_...
- createOpenAI({ baseURL, apiKey }): server-only instantiation

GT route mapping:
- GET /v1/models (native): Optional server fetch to `/v1/models` to populate UI model picker
- POST /v1/chat/completions (native): `streamText` / `generateText` with OpenAI provider → `/v1/chat/completions`
- POST /v1/embeddings (native): `embed` helper with OpenAI provider when RAG routes need `/v1/embeddings`
- POST /v1/audio/transcriptions (not_supported): Not covered by default AI SDK OpenAI chat provider
- POST /v1/audio/speech (not_supported): Not covered by default AI SDK OpenAI chat provider
- POST /v1/images/generations (not_supported): Use experimental image helpers only with image-scoped GT keys
- POST /v1/conversations/files (gt_extension): Server Route Handler multipart to `/v1/conversations/files`
- POST /v1/datasets/{id}/files (gt_extension): Server automation to `/v1/datasets/{id}/files` when needed
- GET /v1/files/{id} (gt_extension): Server polling `GET /v1/files/{id}`

Not supported in this product:
- Vercel AI SDK Responses API (`openai.responses`) is not the GT-validated chat surface — use Chat Completions provider methods.
- Client Components cannot safely hold GT bearer keys; keep all GT calls server-side.

Prerequisites:
- Publish the alias the UI should display as its model name.
- Create conversation-app key (linked inference + upload keys) when chat and files share one external credential.

Setup steps:
1. Add server-only env `GT_API_BASE_URL=${GT_BASE}` and `GT_API_KEY=gtak_...`.
2. Instantiate `createOpenAI({ baseURL: process.env.GT_API_BASE_URL, apiKey: process.env.GT_API_KEY })`.
3. Call `streamText({ model: openai('<published-alias>'), messages })` from a Route Handler.
4. On thread start, `POST /v1/conversations` server-side and attach returned id to subsequent requests.

GT extensions and caveats:
- Upload attachments with `POST /v1/conversations/files` and the same conversation header from server code.
- Poll `GET /v1/files/{id}` before attaching file content to model context.

Validation checklist:
- Client receives streamed tokens without leaking the GT API key.
- Follow-up turns reuse the same GT conversation id.
- File upload + ready polling works for conversation-scoped attachments.
```
