# Dashboard

## Start Here

1. Open **Dashboard** after sign-in.
2. Scan health, version, and alert cards first.
3. Drill into failing components before changing configuration elsewhere.

## Why this matters

The dashboard is the first stop for whether the deployment is safe to change or needs incident response.

## Details

The Control Panel dashboard is the operator landing page for deployment posture. It is intentionally compact: use it to confirm the current state quickly, then move into the specific admin workspace that needs action.

## What the current dashboard shows

The active Gen 3 dashboard summarizes:

- total users
- enabled users
- license status
- license seat usage
- license expiry

It also exposes quick links into the highest-value admin pages.

## When to use the dashboard

Use it at the start of an operator session to answer questions like:

- Is the deployment licensed and healthy enough for routine operations?
- Are user counts or license seats higher than expected?
- Which admin page should I open next?

## What the dashboard is not

The dashboard is not a full operational console. It does not replace the detailed pages for:

- [Users](gen3-admin/users)
- [License](gen3-admin/licenses)
- [Financial Controls](gen3-admin/financial-controls)
- [Settings](gen3-admin/settings)

## Recommended operator pattern

1. Check the dashboard summary.
2. Identify the area that needs action.
3. Move immediately into the dedicated workspace.
4. Return later only for a fresh top-level posture check.

## Best practices

- Treat the dashboard as a quick posture checkpoint, not a place for deep configuration.
- Use the license stats here as an early warning, then confirm details on [License](gen3-admin/licenses).
- Use the user totals here as a summary, then move to [Users](gen3-admin/users) for actual changes.

## Related pages

- [Users](gen3-admin/users)
- [License](gen3-admin/licenses)
- [Financial Controls](gen3-admin/financial-controls)
