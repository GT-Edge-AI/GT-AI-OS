# Storage Pricing (Financial Controls)

## Start Here

1. Open **Financial Controls** from the Control Panel sidebar.
2. Select the **Storage Pricing** tab [route: /dashboard/billing?tab=storage|Storage Pricing tab].
3. Review each **Meter** row (dataset and document GiB-month meters).
4. Set **Price / GiB-month** and confirm **Active** is enabled for meters you bill against.
5. Click **Save storage pricing**.
6. Have a tenant owner confirm the **Storage** line on [Observability](gen3/observability) → **Billing** after retained content accumulates.

## Why this matters

Inference pricing does not include long-lived datasets and documents. Storage meters apply a deployment-wide unit price per gibibyte-month so infrastructure-credit burn and tenant billing analytics can show retention cost separately from model tokens.

## Details

Storage pricing is configured on `/dashboard/billing` (tab `storage`). It is independent of [Model Pricing](gen3-admin/financial-controls/model-pricing) and [Infrastructure Balance](gen3-admin/financial-controls) base-fee settings on the same page.

### Default storage meters

GT AI OS ships two hot-storage meters (meter keys are fixed; operators edit display name, unit price, unit label, and active flag):

| Meter key | Default display name | Unit |
| --- | --- | --- |
| `storage.dataset_hot_gib_month` | Dataset storage | USD per GiB-month |
| `storage.document_hot_gib_month` | Document storage | USD per GiB-month |

The page header summarizes **Current configured storage-price total** as the sum of active row **Price / GiB-month** values (a quick sanity check, not a forecast of tenant usage).

### Editing unit prices

For each meter card:

| Field | Editable | Purpose |
| --- | --- | --- |
| **Meter** | No | Stable identifier consumed by metering (`storage.dataset_hot_gib_month`, etc.) |
| **Display name** | Yes | Operator-facing label on this page |
| **Price / GiB-month** | Yes | Dollar amount charged per GiB-month of retained hot storage |
| **Unit** | Yes | Display string (default `USD per GiB-month`) |
| **Active** | Yes | When disabled, the meter should not apply active pricing |

Enter prices with up to six decimal places (`step="0.000001"`). Click **Save storage pricing** to persist; there is no separate “reset online” for storage—policy is fully operator-defined.

Example starting posture (adjust for your environment):

| Meter | Example price / GiB-month |
| --- | --- |
| Dataset storage | `0.15` |
| Document storage | `0.02` |

### Relationship to tenant Billing → Storage

| Surface | Role |
| --- | --- |
| Control Panel **Storage Pricing** | Sets deployment-wide unit rates per meter |
| Tenant [Observability](gen3/observability) → **Storage** tab | Usage and retention analytics (GiB footprint, trends) |
| Tenant [Observability](gen3/observability) → **Billing** tab (owners only) | Settled spend breakdown including **Storage** alongside inference |

Tenant users and managers do not configure prices; they consume analytics. Only **tenant owners** see **Billing**. After you change storage unit prices, owners should refresh **Billing** over a window where dataset/document retention is non-zero to confirm the **Storage** line moves with policy.

Model inference charges on the same **Billing** view come from [Model Pricing](gen3-admin/financial-controls/model-pricing); do not duplicate storage cost in per-model token fields.

### Best practices

- Set storage prices when billing is enabled and you expect chargeback for retained datasets/documents.
- Keep dataset and document meters on different rates if your cost model treats embeddings corpora vs uploaded files differently.
- Document internal rationale in [Financial Controls](gen3-admin/financial-controls) **Financial details** or change tickets—not in tenant-visible copy.
- Review tenant **Storage** tab utilization before raising unit prices (identify stale datasets driving GiB-month burn).
- Coordinate with [Models](gen3-admin/models) embedding defaults when dataset storage grows after catalog changes.

### Troubleshooting

| Symptom | Check |
| --- | --- |
| Billing **Storage** line is zero | Financial controls enabled; meter **Active**; save succeeded; retention actually present in tenant **Storage** tab |
| Storage total on CP page looks wrong | Sum is unit-price catalog only—verify each **Price / GiB-month**, not tenant GiB usage |
| Owners cannot see billing | Role must be tenant owner; managers never receive **Billing** tab per [Observability](gen3/observability) |

### GT Helper

Ask [GT Helper](gen3-admin/instructions-helper):

- “What is the difference between dataset and document storage meters?”
- “Where do tenant owners see storage charges?”
- “How do I disable storage billing for a meter?”

## Related pages

- [Financial Controls](gen3-admin/financial-controls)
- [Model Pricing](gen3-admin/financial-controls/model-pricing)
- [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards)
- [Observability](gen3/observability)
- [Datasets](gen3/datasets)
- [Documents](gen3/documents)
- [GT Helper](gen3-admin/instructions-helper)
