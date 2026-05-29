## Start Here

Point CrewAI OpenAI LLM configuration at GT API for agent loops; keep GT conversation creation and file handling in the orchestration layer wrapping each crew run. Recommended preset: **Conversation app with uploads**.

## Why this matters

This runbook maps **CrewAI** to GT API routes operators actually publish.

## Details

**Compatibility:** OpenAI plus GT extensions · **Category:** Framework and orchestration

### Official documentation

- https://docs.crewai.com/concepts/llms
- https://docs.crewai.com/how-to/llm-connections
- https://docs.crewai.com/concepts/agents

### Configuration fields

- **OPENAI_API_BASE / OPENAI_BASE_URL:** `https://<tenant-host>/api/tenant`
- **OPENAI_API_KEY:** `gtak_...`
- **Agent LLM model:** `published-agent-alias`

### GT route mapping

| GT route | Verdict | Client integration |
| --- | --- | --- |
| `GET /v1/models` | native | Crew reads configured model string; verify allowlist with manual model list call |
| `POST /v1/chat/completions` | native | CrewAI OpenAI LLM backend posts to `/v1/chat/completions` |
| `POST /v1/embeddings` | not_supported | Not default CrewAI path — add custom tooling if embed scope is required |
| `POST /v1/audio/transcriptions` | not_supported | Not supported via standard CrewAI OpenAI LLM config |
| `POST /v1/audio/speech` | not_supported | Not supported via standard CrewAI OpenAI LLM config |
| `POST /v1/images/generations` | not_supported | Not supported unless custom tasks call image route |
| `POST /v1/conversations/files` | gt_extension | Custom crew tool HTTP multipart with GT headers |
| `POST /v1/datasets/{id}/files` | gt_extension | Custom crew tool targeting dataset upload route |
| `GET /v1/files/{id}` | gt_extension | Custom tool polling `/v1/files/{id}` |

### Not supported in this product

- CrewAI does not natively manage GT conversation headers or dataset multipart uploads.

### Prerequisites

- Publish the alias agents should share across crew roles.
- Decide stateless vs GT conversation-per-session before enabling uploads.

### Setup steps

1. Export `OPENAI_API_BASE=${GT_BASE}` and `OPENAI_API_KEY=gtak_...` in the crew runner environment.
2. Configure each agent LLM with the published alias model name.
3. Run a single-task crew completion before multi-agent autonomy.
4. If files are required, add a custom tool that calls GT upload routes with bearer auth.

### GT extensions and caveats

- Store GT conversation ids in crew session state external to CrewAI memory defaults.
- Use `/v1/conversations/files` when uploads must follow the same GT thread as chat.

### Validation checklist

- All crew roles complete with the same published alias boundary.
- GT conversation id lifecycle is logged when persistence is enabled.
- Upload tasks use GT routes, not assumed OpenAI vendor file APIs.

### Plain-text export

```text
CrewAI runbook
OpenAI plus GT extensions · Framework and orchestration
Recommended key preset: Conversation app with uploads
Evidence: documented compatibility (vendor docs cross-check)

Point CrewAI OpenAI LLM configuration at GT API for agent loops; keep GT conversation creation and file handling in the orchestration layer wrapping each crew run.

Official documentation:
- https://docs.crewai.com/concepts/llms
- https://docs.crewai.com/how-to/llm-connections
- https://docs.crewai.com/concepts/agents

Configuration fields:
- OPENAI_API_BASE / OPENAI_BASE_URL: https://<tenant-host>/api/tenant
- OPENAI_API_KEY: gtak_...
- Agent LLM model: published-agent-alias

GT route mapping:
- GET /v1/models (native): Crew reads configured model string; verify allowlist with manual model list call
- POST /v1/chat/completions (native): CrewAI OpenAI LLM backend posts to `/v1/chat/completions`
- POST /v1/embeddings (not_supported): Not default CrewAI path — add custom tooling if embed scope is required
- POST /v1/audio/transcriptions (not_supported): Not supported via standard CrewAI OpenAI LLM config
- POST /v1/audio/speech (not_supported): Not supported via standard CrewAI OpenAI LLM config
- POST /v1/images/generations (not_supported): Not supported unless custom tasks call image route
- POST /v1/conversations/files (gt_extension): Custom crew tool HTTP multipart with GT headers
- POST /v1/datasets/{id}/files (gt_extension): Custom crew tool targeting dataset upload route
- GET /v1/files/{id} (gt_extension): Custom tool polling `/v1/files/{id}`

Not supported in this product:
- CrewAI does not natively manage GT conversation headers or dataset multipart uploads.

Prerequisites:
- Publish the alias agents should share across crew roles.
- Decide stateless vs GT conversation-per-session before enabling uploads.

Setup steps:
1. Export `OPENAI_API_BASE=${GT_BASE}` and `OPENAI_API_KEY=gtak_...` in the crew runner environment.
2. Configure each agent LLM with the published alias model name.
3. Run a single-task crew completion before multi-agent autonomy.
4. If files are required, add a custom tool that calls GT upload routes with bearer auth.

GT extensions and caveats:
- Store GT conversation ids in crew session state external to CrewAI memory defaults.
- Use `/v1/conversations/files` when uploads must follow the same GT thread as chat.

Validation checklist:
- All crew roles complete with the same published alias boundary.
- GT conversation id lifecycle is logged when persistence is enabled.
- Upload tasks use GT routes, not assumed OpenAI vendor file APIs.
```
