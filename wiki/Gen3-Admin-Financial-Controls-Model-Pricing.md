# Model Pricing (Financial Controls)

## Start Here

1. Open **Financial Controls** from the Control Panel sidebar.
2. Select the **Model Pricing** tab [route: /dashboard/billing?tab=models|Model Pricing tab].
3. Confirm each configured model from [Models](gen3-admin/models) appears with a pricing status badge.
4. Filter by **Provider** or **Status** when you need to focus on unresolved rows or one vendor.
5. Use **Reset selected to online defaults** or **Reset all to online defaults** after catalog changes, then click **Save model pricing** when manual edits are complete.
6. Ask a tenant owner to review **Billing** on [Observability](gen3/observability) to confirm settled usage reflects your policy.

## Why this matters

Model pricing turns inference, embedding, speech, and image activity into infrastructure-credit burn tenants see in analytics. If prices drift from provider rate cards—or stay **Unresolved** or **Unsupported**—chargeback, budget warnings, and owner-facing billing summaries become misleading even when usage is healthy.

## Details

The **Model Pricing** workspace lives on the Control Panel **Financial Controls** route (`/dashboard/billing`, tab `models`). It prices every model registered in [Models](gen3-admin/models) → **Configured Models**, including multi-capability models and compound routers such as Groq Compound.

For provider list prices and mapping examples, see [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards). For retained-content meters, see [Storage pricing](gen3-admin/financial-controls/storage-pricing). For the full billing-policy surface, see [Financial Controls](gen3-admin/financial-controls).

### Workspace layout

| Area | Purpose |
| --- | --- |
| Search | Filter by provider name, model name, or model key (press **Enter** to apply) |
| Provider | Restrict to one inference provider |
| Status | Filter by pricing status or enabled/disabled |
| Sort | Order by provider, model, input price, output price, or status |
| Table | One row per configured model with expandable capability pricing |
| Bulk actions | Export, import, clear, reset online, save |

The summary bar reports how many model rows are configured, how many are active, and how many are selected on the current page.

### Pricing status meanings

| Status | Meaning | Typical next step |
| --- | --- | --- |
| **Auto-priced** | GT AI OS resolved a price from an online catalog snapshot (OpenRouter and/or LiteLLM) | Review after provider price changes; re-run online reset if needed |
| **Manual** | An operator entered or imported prices, or disabled a row | Document **Source / notes**; keep aligned with your rate-card policy |
| **Unresolved** | No online source matched, or catalog fetch failed | Enter manual token or unit prices, enable the row, save; or fix model key/provider mapping |
| **Unsupported** | Online catalog has the model but not in a meter shape GT AI OS can apply (for example non-token image rates) | Enter manual **unit price** for the capability, enable, save |

Status badges appear on the model row. When **pricingStatusReason** is set (for example `model not found in litellm catalog`), it prints under the badge.

Rows that are **Unresolved**, **Unsupported**, or **Disabled** show guidance: enter manual pricing, keep **Enabled** on, and save to use the model for inference billing.

### Online pricing sources

When you reset to online defaults, the Control Panel backend refreshes cached snapshots (about 12-hour TTL) and resolves each capability profile:

| Source | URL | Used when |
| --- | --- | --- |
| OpenRouter catalog | `https://openrouter.ai/api/v1/models` | Provider type or name is OpenRouter |
| LiteLLM model catalog | `https://api.litellm.ai/model_catalog` | Primary non-OpenRouter resolution |
| LiteLLM raw JSON | `https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json` | Fallback when the API catalog does not match |

OpenRouter is consulted first for OpenRouter providers. Other providers use LiteLLM catalog, then the raw GitHub JSON. Manual rows are preserved on background sync unless you force an online reset.

### Reset to online defaults workflow

1. Optionally filter to the provider or status you care about.
2. Select rows with checkboxes, or rely on filter-scoped reset:
   - **Reset selected to online defaults** — only checked rows on the current result set.
   - **Reset all matching to online defaults** — every row matching active search/provider/status filters (confirmation dialog).
   - **Reset all to online defaults** — entire catalog when no filters are active.
3. Read the notice summary (`auto-priced`, `unresolved`, `unsupported` counts).
4. Review rows that stayed unresolved; add manual prices where needed.
5. Click **Save model pricing** to persist (reset updates server state, but treat unsaved local edits separately if you changed cells before saving).

Reset replaces manual prices **when** an online source resolves the row. It does not invent prices for unsupported metering shapes.

### Manual override workflow

1. Locate the model row (search or provider filter).
2. For **token I/O** capabilities, set **Input token price / 1M** and **Output token price / 1M**.
3. For **audio duration**, **input characters**, or **image count** capabilities, set the **unit price** field (audio price per hour, input characters per 1M, or price per generated image).
4. Optionally fill **Source / notes** (`priceSource`) with your internal reference or provider doc link.
5. Ensure **Enabled** is checked.
6. Click **Save model pricing**.

Typing prices marks the capability **Manual** in the UI draft. Saving writes the catalog version tenants consume.

### Capability rows (request types)

Each configured model can expose one or more capability rows derived from model capabilities in [Models](gen3-admin/models):

| Request type (`requestType`) | Operator label | Pricing method | Fields you edit |
| --- | --- | --- | --- |
| `chat` | chat | token I/O | Input / output per 1M tokens |
| `embed` | embed | token I/O | Input / output per 1M tokens (output often `0`) |
| `image_analysis` | image analysis | token I/O | Input / output per 1M tokens |
| `transcription` | transcription | audio duration (`audio_seconds`) | Unit price (USD per hour; runtime meters audio seconds) |
| `speech_synthesis` | speech synthesis | input characters | Unit price (USD per 1M input characters) |
| `image_generation` | image generation | image count | Unit price (USD per generated image) |

Additional normalized types (`translation`, `web_search`) follow the same catalog rules when present on a model.

The **Capabilities** and **Method** columns summarize request type, pricing method, billing unit, and rounding policy (for example **ceil to second** for STT, **whole image** for image generation).

### Compound model rows

**Groq Compound** (`groq/compound`) and similar compound routers show **Groq Compound underlying model overrides**. Each underlying model lists:

- Display name and model key
- Whether pricing comes from a **configured model** row or **manual** override
- Per-underlying input and output token price per 1M

Configure prices for underlying models in [Models](gen3-admin/models) when possible; use compound overrides when chargeback must differ from the child model catalog row.

### CSV bulk edit

**Export all** or **Export selected** downloads a CSV with canonical columns:

`modelId`, `modelKey`, `providerName`, `modelName`, `requestType`, `pricingMethod`, `billingUnit`, `unit`, `unitPrice`, `priceSource`, `pricingStatus`, `pricingStatusReason`, `inputPricePerMillion`, `outputPricePerMillion`, `currency`, `active`

**Import CSV** merges into the current workspace by `modelId` or `modelKey`, optionally scoped with `requestType` for multi-capability models. Unmatched references are skipped and reported in the notice.

Aliases accepted on import include `provider`, `input_price_per_million`, `output_price_per_million`, `pricing_status`, `enabled` → `active`, and similar snake_case forms.

After import: review statuses, fix unmatched keys, click **Save model pricing**.

**Clear selected** removes prices on checked rows (sets unresolved-style empty pricing in the draft); save only if that is intentional.

### When to save

| Action | Save required? |
| --- | --- |
| Edit input/output/unit prices in the grid | Yes — **Save model pricing** |
| Toggle **Enabled** | Yes |
| Import CSV | Yes (import updates draft state; notice reminds you) |
| Reset to online defaults | Server applies reset immediately; still review and save if you combine with local edits |
| Export CSV | No |

Read-only sessions (non–Super Admin or read-only license posture) disable save, reset, and import.

### Verify in tenant Observability

Configuration is Control Panel–only. Validation is tenant-side:

1. Ensure **Financial controls** are enabled and infrastructure credits are funded on [Financial Controls](gen3-admin/financial-controls) → **Infrastructure Balance**.
2. Sign in as a **tenant owner**.
3. Open [Observability](gen3/observability) → **Billing** tab.
4. Compare model and storage breakdowns to the prices you configured after representative usage.

Managers and tenant users do not see the **Billing** tab; use an owner account for verification.

### Best practices

- Reconcile model pricing whenever [Models](gen3-admin/models) gains or changes providers.
- Run **Reset all to online defaults** after major OpenRouter or LiteLLM catalog updates, then manually fix remaining **Unsupported** rows.
- Keep **Source / notes** populated for manual rows (contract ID, rate-card date, or URL).
- Price embeddings and vision capabilities separately when the same model key serves multiple request types.
- Set local/Ollama models to `$0.00` input and output when you intentionally exclude pass-through API cost (see [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards)).

### Troubleshooting

#### Row stays **Unresolved**

- Confirm the model exists and is enabled under [Models](gen3-admin/models).
- Check provider type and model key match the upstream catalog (OpenRouter slugs vs LiteLLM keys).
- Retry **Reset … to online defaults** after cluster egress to the catalog URLs is restored.
- Enter manual prices, enable the row, save.

#### Row is **Unsupported**

- Common when OpenRouter lists image pricing not expressed as per-image counts, or LiteLLM lists transcription/TTS in a non-metered shape.
- Enter the correct **unit price** for that capability method and save as **Manual**.

#### Usage shows $0 or wrong burn

- Verify the row is **Enabled** and saved.
- Confirm tenants use the priced model ID, not an alias bypassing the catalog.
- Check capability row (chat vs embed) matches the request type actually metered.

#### CSV import skipped rows

- Include `modelKey` or `modelId` exactly as in the workspace.
- Add `requestType` when importing a non-chat capability on a multi-capability model.

### GT Helper

From **Financial Controls** → **Pricing Guides** or the **?** shelf, ask [GT Helper](gen3-admin/instructions-helper) questions such as:

- “How do I fix unresolved pricing for Azure OpenAI gpt-4o?”
- “What CSV columns do I need to bulk-update embedding prices?”
- “When should I reset model pricing to online defaults?”

## Related pages

- [Financial Controls](gen3-admin/financial-controls)
- [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards)
- [Storage pricing](gen3-admin/financial-controls/storage-pricing)
- [Models](gen3-admin/models)
- [Observability](gen3/observability)
- [GT Helper](gen3-admin/instructions-helper)
