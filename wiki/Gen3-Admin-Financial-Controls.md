# Financial Controls

## Start Here

1. Open **Financial Controls**.
2. Review base infrastructure fee fields separately from usage pricing.
3. Update model pricing tables when [Models](gen3-admin/models) catalog changes.
4. Lock or document explanatory notes before saving billing changes.

## Why this matters

Financial controls affect chargeback and budgets—separate base fees from variable usage to avoid silent policy drift.

## Details

`Financial Controls` is the active Gen 3 billing-policy workspace. It combines billing enablement, budget posture, model pricing, storage pricing, and allocation management on one Control Panel route.

## What the current page supports

The live page includes:

- billing status review
- billing enable/disable control
- budget and enforcement policy
- model-pricing configuration
- storage-pricing configuration
- allocation creation and review

## Major sections

### Billing status

Use this section to confirm whether billing is enabled and whether the deployment has the license posture needed for billing-aware workflows.

### Budget settings

Use budget settings to define warning, critical, or hard-stop posture and the general enforcement model for the deployment's infrastructure-credit or budget behavior.

### Model pricing

This section controls the prices attached to configured models. Keep it aligned with the actual provider catalog so observability and budget posture remain meaningful.

Deep-dive runbooks:

- [Model Pricing workspace](gen3-admin/financial-controls/model-pricing) — statuses, online reset, CSV import/export, capability and compound rows
- [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards) — vendor list-price URLs and mapping into input/output per 1M tokens or unit pricing

### Storage pricing

Use storage-pricing controls when the deployment tracks retained content cost as part of billing posture.

See [Storage pricing](gen3-admin/financial-controls/storage-pricing) for dataset/document GiB-month meters and tenant **Billing** verification.

### Allocations

Use allocations to divide or label spending posture in a more structured way than a single shared pool.

## Recommended operator workflow

1. Confirm billing is enabled only when the deployment is ready for it.
2. Review the budget policy.
3. Update model prices after any material provider-catalog change.
4. Review storage-pricing assumptions.
5. Create or adjust allocations only after the baseline policy is sound.

## What this page does not do

- It does not activate the enterprise license. Use [License](gen3-admin/licenses).
- It does not manage the underlying inference provider connectivity. Use [Models](gen3-admin/models).

## Best practices

- Change pricing soon after provider or model changes so analytics stay trustworthy.
- Treat enforcement posture as an operational policy decision, not just a UI toggle.
- Review tenant-facing billing analytics after major policy updates to confirm the outcome is understandable to tenant users.

## Related pages

- [Model Pricing](gen3-admin/financial-controls/model-pricing)
- [Provider rate cards](gen3-admin/financial-controls/provider-rate-cards)
- [Storage pricing](gen3-admin/financial-controls/storage-pricing)
- [Models](gen3-admin/models)
- [Observability](gen3/observability)
- [GT Helper](gen3-admin/instructions-helper)
- [License](gen3-admin/licenses)
