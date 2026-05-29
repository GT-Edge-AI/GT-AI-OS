## Start Here

Use this reference while wiring clients. Poll upload processing with `GET /v1/files/{id}` (alias `GET /v1/uploads/{id}`) until status is `ready` or `failed`.

## Why this matters

GT API mirrors OpenAI-shaped paths under `/api/tenant/v1/*` but adds conversation headers, dataset uploads, and file-status polling documented here.

## Details

OpenAPI source of truth: `gt-ai-os/docs/reference/GT3-TENANT-EXTERNAL-API-OPENAPI.yaml`.



### Bearer authentication

**AUTH** `Authorization: Bearer gtak_...`

Every GT API route stays private behind tenant-local bearer-key authentication.

- Keys are shown in plaintext once and then stored only as hashes.
- What a caller can see depends on the key scopes, allowlists, and any linked conversation binding.
- Inference keys may attach prompt guardrail modules and additional prompt text; GT applies those layers server-side together with the configured agent (or raw-model routing policy) for allowed calls.

```bash
Authorization: Bearer <YOUR_GT_API_KEY>
Content-Type: application/json
```

### List published models

**GET** `/v1/models`

Returns only the published inference aliases the presented key is allowed to discover.

- Each entry is a published inference name callers put in `model`, not a bearer secret.
- The list can include agent-backed aliases and operator-published raw-model catalog names; both are filtered by the presenting key’s allowlists before they appear.
- They only appear to requests that already present a valid scoped API key.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  "https://<tenant-host>/api/tenant/v1/models"
```

### Create embeddings

**POST** `/v1/embeddings`

Runs an OpenAI-compatible embeddings request using a published alias while GT resolves the tenant embedding model behind the trust boundary.

- The presented key must include `inference:embed` for the allowlisted name.
- The public `model` stays a published agent alias or raw-model catalog name; GT still resolves embeddings through the tenant trust boundary when routing uses an agent-backed alias.
- Use `encoding_format: "float"` or `encoding_format: "base64"` depending on what the client library expects.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/embeddings" \
  -d '{
    "model": "agent-alias",
    "input": ["Mission objective", "Known risks"]
  }'
```

### Run a chat completion

**POST** `/v1/chat/completions`

Runs an OpenAI-compatible chat request using a published model alias.

- Send the user content you want the model to answer; for agent aliases, the configured agent supplies its base prompt, and the key may add prompt modules or extra prompt text on top.
- `model` must be a published name this key may use: an agent alias or a published raw-model catalog name.
- Without `X-GT-Conversation-Id`, chat completions stay stateless and do not create a persisted GT conversation.
- Clients that need GT-managed continuity should call `POST /v1/conversations` first, then reuse the returned `X-GT-Conversation-Id` header on follow-up chat and upload requests.
- Conversation-facing keys may inherit their runtime allowlists from linked inference and upload keys.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/chat/completions" \
  -d '{
    "model": "agent-alias",
    "messages": [
      { "role": "user", "content": "Summarize the attached mission brief." }
    ]
  }'
```

### Transcribe audio

**POST** `/v1/audio/transcriptions`

Runs OpenAI-compatible speech-to-text using the published agent alias and that agent's configured STT model.

- The presented key must include `inference:transcribe` for the allowlisted alias.
- The public `model` stays an exposed agent alias; GT resolves the underlying STT model behind the tenant trust boundary.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -F "model=agent-alias" \
  -F "file=@call.wav" \
  "https://<tenant-host>/api/tenant/v1/audio/transcriptions"
```

### Generate speech

**POST** `/v1/audio/speech`

Runs OpenAI-compatible text-to-speech using the published agent alias and that agent's configured TTS model.

- The presented key must include `inference:speech` for the allowlisted alias.
- Agent speech settings can supply the default voice and output format when the request omits them.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/audio/speech" \
  -d '{
    "model": "agent-alias",
    "input": "Read the mission summary aloud."
  }'
```

### Generate an image

**POST** `/v1/images/generations`

Runs OpenAI-compatible image generation using the published agent alias and that agent's configured image model.

- The presented key must include `inference:image` for the allowlisted alias.
- Dataset `vision_model` is unrelated here; it remains an ingestion/indexing setting, not a runtime generation selector.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/images/generations" \
  -d '{
    "model": "agent-alias",
    "prompt": "Create a satellite-style map of the extraction zone."
  }'
```

### Create a GT conversation

**POST** `/v1/conversations`

Creates a GT-managed conversation id for clients that want persisted chat continuity and conversation-scoped uploads.

- This is a GT-specific extension; ordinary OpenAI-compatible clients can stay on stateless `/v1/chat/completions`.
- `model` must be a published inference name that the presented key is allowed to use (agent alias or raw-model catalog name).

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/conversations" \
  -d '{
    "model": "agent-alias",
    "title": "Evidence review thread"
  }'
```

### Upload into a dataset target

**POST** `/v1/datasets/{id}/files`

Accepts multipart file uploads for a static dataset target allowed by the presented upload key.

- Use this for direct dataset ingestion flows.
- The key must carry `datasets:write` and be allowed to reach that dataset target.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -F "file=@mission-brief.pdf" \
  "https://<tenant-host>/api/tenant/v1/datasets/reference-briefs/files"
```

### Upload into a conversation flow

**POST** `/v1/conversations/files`

Accepts multipart file uploads that auto-create and attach a conversation-scoped dataset rather than targeting a fixed dataset alias.

- Requires `X-GT-Conversation-Id`.
- The key must allow conversation-scoped uploads, either directly or through a linked upload key.
- The upload creates or reuses the conversation upload dataset that stays attached to the active chat scope.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "X-GT-Conversation-Id: <GT_CONVERSATION_ID>" \
  -F "file=@evidence-photo.png" \
  "https://<tenant-host>/api/tenant/v1/conversations/files"
```

### Poll file processing status

**GET** `/v1/files/{fileId}`

Returns asynchronous processing state for a previously uploaded file.

- Use this after either dataset or conversation uploads when downstream processing is asynchronous.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  "https://<tenant-host>/api/tenant/v1/files/<FILE_ID>"
```

### Conversation continuity header

**HEADER** `X-GT-Conversation-Id`

Carries the GT conversation id that ties follow-up chat turns and conversation-scoped uploads together.

- Required for `/v1/conversations/files`.
- Optional on `/v1/chat/completions`; when present, GT API uses the existing persisted conversation instead of stateless request history only.
- Returned by `POST /v1/conversations` so clients can opt into persisted chat continuity explicitly.

```bash
curl -sS \
  -H "Authorization: Bearer <YOUR_GT_API_KEY>" \
  -H "X-GT-Conversation-Id: <GT_CONVERSATION_ID>" \
  -H "Content-Type: application/json" \
  "https://<tenant-host>/api/tenant/v1/chat/completions" \
  -d '{
    "model": "agent-alias",
    "messages": [
      { "role": "user", "content": "Use the same conversation context for this follow-up." }
    ]
  }'
```
