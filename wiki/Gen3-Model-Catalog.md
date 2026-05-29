# Model Catalog

## Start Here

1. Open **Management → Model Catalog** from the tenant sidebar (alongside **Observability**, **Users**, and **Groups** when those routes are visible to your role).
2. Read the **Default model by capability** strip at the top to see which models are currently marked default for chat, embeddings, vision, speech-to-text, text-to-speech, and image generation.
3. Use search and the filter dropdowns to narrow the catalog table when you need a specific provider, model type, default status, source, or country.
4. Click a column header to sort; use **Reset all** when filters hide the model you expected.
5. When you need to change what appears here, ask a Control Panel operator to update [Models](gen3-admin/models)—this tenant page is browse-only.

## Why this matters

Model Catalog is the read-only inventory of inference models published to your tenant. It helps you confirm which chat, embedding, vision, speech, and image models are available—and which ones are marked as deployment defaults—before you configure [Agents](gen3/agents) or interpret model choices in chat and [GT API](gen3/gt-api/overview).

## Details

The tenant `Model Catalog` route (`/model-catalog`) lists inference models the deployment exposes to this tenant. The page does not add, remove, or edit models. The hero note states: **Browse only. Catalog changes are made from the control panel.**

All signed-in tenant roles (**Tenant User**, **Tenant Manager**, and **Tenant Owner**) can open Model Catalog when it appears under **Management**. Unlike **Users**, Model Catalog is not role-gated off the management menu.

![Tenant Model Catalog browse table and default strip](gen3/images/model-catalog.png)

## Where to find it

| Item | Value |
| --- | --- |
| Route | `/model-catalog` |
| Sidebar label | **Model Catalog** |
| Nav section | **Management → Model Catalog** (with **Observability**, **Users**, **Groups**) |
| Page eyebrow | Inference |
| Page title | Model catalog |

Management nav order in the sidebar: **Observability** (when your role can view it), **Users** (owners and managers only), **Groups**, then **Model Catalog**.

## What the page shows

### Hero summary

When models load successfully, the header shows summary chips:

- **Total models** — unique models in the catalog
- **Providers** — distinct provider count
- **Rows with a default** — models that carry at least one default badge
- **Showing X of Y** — appears while filters are active

### Default model by capability strip

Below the summary, a compact strip lists one row per catalog capability intent:

| Capability | Internal intent |
| --- | --- |
| Chat | `chatText` |
| Embeddings | `embedText` |
| Vision | `visionDescribe` |
| Speech-to-text | `transcribeAudio` |
| Text-to-speech | `synthesizeSpeech` |
| Image generation | `generateImage` |

Each cell shows the default model name(s) for that capability, formatted as `[Provider] Model name` when provider metadata exists. When no default is configured for that slice, the cell reads **No default set**.

Default badges follow this precedence:

1. **Control Panel deployment defaults** — when the operator configured a default model id for that capability (`/deployment-default-models`), matching catalog rows receive a default badge for that intent.
2. **Resource-cluster slice default** — when no Control Panel default id is set for an intent, a model marked `isDefault` in the per-intent inference list can receive the badge instead.

### Catalog table

The table lists one row per unique model (deduplicated across intents). Columns:

| Column | Content |
| --- | --- |
| **Model** | Display name (with provider prefix when available) and default badges such as `Default · Chat` |
| **Provider** | Provider name or id |
| **Model type** | Intent chips (Chat, Embeddings, Vision, and so on); chips highlight when that intent is a default for the row |
| **Model source** | Published source metadata when present |
| **Country of origin** | Country metadata when present |
| **Capabilities** | Summarized input/output modalities plus flags such as streaming, tools, embeddings, STT, and TTS |

Empty metadata cells show an em dash (`—`).

## Filters and sort

### Search

The search field matches (case-insensitive) against model name, model id, provider, model type labels, default badge text, capability summary, source, and country.

### Filter dropdowns

| Filter | Options |
| --- | --- |
| **Provider** | All providers, or one provider from the loaded catalog |
| **Model type** | All model types, or one intent (Chat, Embeddings, Vision, Speech-to-text, Text-to-speech, Image generation) |
| **Default status** | All rows, **Defaults only**, or **No default badges** |
| **Model source** | All sources, or one source from the loaded catalog |
| **Country** | All countries, or one country from the loaded catalog |

When any filter or search is active, **Reset all** clears every filter and the search box. A meta pill shows how many models match (`N models match` or `N models listed`).

### Sort

Click a column header to sort by **Model**, **Provider**, **Model type**, **Model source**, **Country of origin**, or **Capabilities**. Click the same header again to reverse direction. The active column shows an ascending or descending indicator.

## Default badges in the table

Models marked default for one or more intents show chips under the model name, for example `Default · Chat` or `Default · Embeddings`.

In the **Model type** column, intent chips use a highlighted style when that intent is a default for the row. Column meta text reads **Has default badge** or **No default badge**.

## Empty and error states

- **Loading:** `Loading model catalog…`
- **No models published:** `No inference models are available for this tenant yet.` with guidance that models appear after the operator publishes them.
- **Filters match nothing:** `No models match this filter.` with a hint to try another search or dropdown.
- **Load failure:** an error alert with the API message (for example `Failed to load models.`).

## Who configures vs who browses

| Surface | Role | What you do |
| --- | --- | --- |
| **Model Catalog** (tenant app) | All signed-in tenant roles | Browse models, defaults, providers, and capabilities |
| **Models** (Control Panel) | Operators | Configure inference providers, register models, and set deployment-wide defaults |
| **Agents** (tenant app) | All signed-in tenant roles | Pick models inside agent configuration from models available to the tenant—not from this catalog editor |

Operators work on [Models](gen3-admin/models) across three tabs—**Inference Providers**, **Configured Models**, and **Default Models**. Tenant users see the result in Model Catalog and in agent model pickers.

When an agent or chat workflow uses a model, it draws from the tenant inference registry. Model Catalog helps you verify what the registry contains and which capabilities are marked default before you assign models in [Agents](gen3/agents/building).

## Common tasks

### Confirm which chat model is the deployment default

Open Model Catalog and read the **Chat** cell in the default strip, or filter **Default status** to **Defaults only** and look for `Default · Chat` badges.

### Find all models from one provider

Set **Provider** to that provider and review the table. Use **Model type** if you only need chat or embedding models.

### Compare modality support

Sort or scan the **Capabilities** column. Summaries describe input and output modalities (text, image, audio) and note extras such as streaming, tool use, embeddings, STT, or TTS when the model supports them.

## Best practices

- Treat Model Catalog as reference inventory, not a configuration page.
- Check the default strip when troubleshooting unexpected model behavior in chat or agents.
- Route catalog changes (new providers, imports, default changes) to Control Panel operators via [Models](gen3-admin/models).
- Use filters instead of scrolling when the deployment publishes many models.

## Related pages

- [Agents](gen3/agents)
- [Agents — Building Agents](gen3/agents/building)
- [Control Panel Models](gen3-admin/models)
- [GT API Overview](gen3/gt-api/overview)
- [Getting Started](gen3/getting-started)
