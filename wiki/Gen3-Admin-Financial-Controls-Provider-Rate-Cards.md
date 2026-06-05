# Provider Rate Cards (Financial Controls)

## Start Here

1. Open the vendor’s official pricing page from the table below.
2. Map list prices into [Model Pricing](gen3-admin/financial-controls/model-pricing) fields on [Financial Controls](gen3-admin/financial-controls) [route: /dashboard/billing?tab=models|Model Pricing tab].
3. Prefer **Reset … to online defaults** when OpenRouter or LiteLLM already lists the model; use manual entry for private endpoints, negotiated rates, or unsupported metering.
4. Document the source in each row’s **Source / notes** field.
5. Save model pricing and validate spend on tenant [Observability](gen3/observability) → **Billing**.

## Why this matters

Provider rate cards change frequently. GT AI OS does not substitute your commercial contract—it gives you a structured place to mirror what you pay (or what you charge back) per token, audio second, character, or image. Mapping vendor units correctly prevents systematic under- or over-charging in infrastructure credits and tenant billing analytics.

## Details

Use this article with [Model Pricing](gen3-admin/financial-controls/model-pricing) for workspace mechanics and [Financial Controls](gen3-admin/financial-controls) for infrastructure balance and storage meters.

### Major providers and official pricing docs

| Provider | Typical GT AI OS provider type | Official pricing documentation |
| --- | --- | --- |
| OpenAI | `openai` | [OpenAI API pricing](https://openai.com/api/pricing/) |
| Anthropic | `anthropic` | [Anthropic pricing](https://www.anthropic.com/pricing) |
| Google / Gemini | `google`, `vertex`, `gemini` | [Google AI Gemini API pricing](https://ai.google.dev/pricing) |
| Azure OpenAI | `azure` | [Azure OpenAI Service pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/) |
| AWS Bedrock | `bedrock` | [Amazon Bedrock pricing](https://aws.amazon.com/bedrock/pricing/) |
| Mistral | `mistral` | [Mistral AI pricing](https://mistral.ai/technology/#pricing) |
| Groq | `groq` | [Groq pricing](https://groq.com/pricing) |
| Local / Ollama | `ollama`, on-prem adapters | No public API list price—use `$0.00` token rates unless you allocate internal cost |
| OpenRouter | `openrouter` | [OpenRouter pricing](https://openrouter.ai/docs/pricing) (also exposed via `https://openrouter.ai/api/v1/models`) |

Always confirm region, enterprise discount, and cached-token pricing on the vendor site before you lock GT AI OS numbers.

### Map provider rate card → Financial Controls fields

| Vendor publishes | GT AI OS field | Notes |
| --- | --- | --- |
| $/1M input tokens | **Input token price / 1M** | Chat, embed, vision (`image_analysis`) capabilities |
| $/1M output tokens | **Output token price / 1M** | Chat and vision; often `0` for embeddings |
| $/minute or $/hour audio | **Audio price / hour** on `transcription` rows | Runtime meters **audio_seconds**; LiteLLM may supply per-second costs converted to hourly display |
| $/1M characters (TTS) | **Input character price / 1M** on `speech_synthesis` | Maps to `input_characters` pricing method |
| $/image | **Image price / generated image** on `image_generation` | Per-image `image_count` method |
| Model not in online catalogs | Manual input/output or unit price + **Enabled** | Status becomes **Manual** after save |

CSV import uses the same columns: `inputPricePerMillion`, `outputPricePerMillion`, `unitPrice`, `requestType`, `pricingMethod`, `priceSource`, `active`. See [Model Pricing](gen3-admin/financial-controls/model-pricing) for the full column list.

### Example: OpenAI GPT-4o (chat)

Public list pricing (verify on [OpenAI API pricing](https://openai.com/api/pricing/) before you save):

| Vendor list price | Financial Controls value |
| --- | --- |
| $5.00 / 1M input tokens | Input token price / 1M = `5.00` |
| $15.00 / 1M output tokens | Output token price / 1M = `15.00` |

Set **Source / notes** to `OpenAI API pricing – GPT-4o – YYYY-MM-DD`. Request type `chat`, pricing method **token I/O**.

### Example: Anthropic Claude Sonnet–class (chat)

Anthropic publishes separate input and output token rates (verify on [Anthropic pricing](https://www.anthropic.com/pricing/)):

| Vendor list price (illustrative) | Financial Controls value |
| --- | --- |
| $3.00 / 1M input tokens | Input token price / 1M = `3.00` |
| $15.00 / 1M output tokens | Output token price / 1M = `15.00` |

Use the exact model name/key from [Models](gen3-admin/models) (`claude-sonnet-4-…`, etc.) so online reset and CSV import align.

### Example: Embeddings

| Vendor list price | Financial Controls value |
| --- | --- |
| $0.13 / 1M input tokens (text-embedding-3-large) | Input token price / 1M = `0.13` on `embed` capability |
| No output charge | Output token price / 1M = `0.00` |

### Example: Speech and images

| Capability | Vendor unit | Financial Controls |
| --- | --- | --- |
| STT | Vendor $/minute → convert to $/hour if the UI labels hourly | **Audio price / hour** on `transcription` |
| TTS | Vendor $/1M characters | **Input character price / 1M** on `speech_synthesis` |
| Image gen | Vendor $/image | **Image price / generated image** on `image_generation` |

When online reset marks a row **Unsupported**, the vendor doc still lists a price but GT AI OS cannot ingest that shape automatically—enter the unit field manually.

### Reset to online defaults vs manual entry

| Situation | Recommended approach |
| --- | --- |
| Model routed through **OpenRouter** with public catalog entry | **Reset … to online defaults** (OpenRouter snapshot first) |
| Direct OpenAI / Anthropic / Groq / Bedrock with LiteLLM coverage | **Reset … to online defaults** (LiteLLM API + raw JSON fallback) |
| Enterprise Azure deployment with private rates | Manual entry from your Azure rate card |
| Local **Ollama** / on-prem GPU | Manual `$0.00` / `$0.00` unless you allocate internal chargeback |
| Negotiated discount not reflected in public catalogs | Manual entry; note contract in **Source / notes** |
| Row **Unsupported** after reset | Manual unit or token prices |

Online sources:

- `https://openrouter.ai/api/v1/models`
- `https://api.litellm.ai/model_catalog`
- `https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json`

Manual rows are preserved during background model sync until you run an online reset on those rows.

### Compound and multi-vendor models

- **Groq Compound** (`groq/compound`): price underlying models in [Model Pricing](gen3-admin/financial-controls/model-pricing) or override in the compound section; see [Model Pricing](gen3-admin/financial-controls/model-pricing) compound discussion.
- **OpenRouter** slugs (`openai/gpt-4o`): ensure provider type is OpenRouter so reset uses the OpenRouter catalog.

### Best practices

- Date-stamp **Source / notes** when vendors change list prices.
- Re-run online reset after LiteLLM or OpenRouter catalog updates, then diff remaining manual rows.
- Align [Models](gen3-admin/models) model keys with vendor IDs before importing CSV.
- Use [Storage pricing](gen3-admin/financial-controls/storage-pricing) for GiB-month retention; do not mix storage into token rows.

### GT Helper example questions

Ask [GT Helper](gen3-admin/instructions-helper) from **Pricing Guides** or the **?** shelf:

- “Map Azure OpenAI gpt-4o mini list prices to Financial Controls input and output per million.”
- “Should I use online reset or manual pricing for Bedrock Claude on a private account?”
- “What price should I set for local Ollama llama3 in model pricing?”
- “How do I enter Groq Whisper STT pricing when the row is unsupported?”

## Related pages

- [Model Pricing](gen3-admin/financial-controls/model-pricing)
- [Financial Controls](gen3-admin/financial-controls)
- [Storage pricing](gen3-admin/financial-controls/storage-pricing)
- [Models](gen3-admin/models)
- [Observability](gen3/observability)
- [GT Helper](gen3-admin/instructions-helper)
