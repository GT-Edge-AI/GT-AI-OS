# Group Spend

## Start Here

1. Sign in as a **tenant owner**. The **Billing** tab is owner-only.
2. Open **Management → Observability**.
3. Set **Time range**. Choose **All time** when you want the full retained window. Reports and exports use that selection.
4. Open **Billing**.
5. Use the **Group** filter, or click a bar on the **Group spend** chart, to limit the view to people in that group.

## Why this matters

Group spend shows total inference spend for the people in each group, including a named chart. **All time** covers the retained history. Exports follow the same time range you selected on the page.

## Details

**Billing** is analytic. Pricing and budgets are set in Control Panel [Financial Controls](gen3-admin/financial-controls). Tenant managers use the **Managed group** filter on the tabs they can open. They do not see **Billing**.

### Group spend chart

The chart title is **Group spend**. The subtitle states: total inference spend for people in each group. Click a bar to apply the **Group** filter above. People in more than one group are counted in each group.

With a group selected, the user chart subtitle describes inference spend by people associated with that group. That is their metered usage in the selected timeframe, including requests that did not use this group’s shared agents.

### Time range

**Time range** options are **All time**, **Today**, **Last 7 days**, and **Last 30 days**. Choose the range before you export. **All time** is sent with the report and export so the download matches the on-screen range.

### Top managers

**Top managers** lists spend tied to a group manager budget. **No assigned manager** means the request was not charged to one.

When one agent is shared into more than one managed group, a caller who belongs to exactly one of those groups’ budget pools is charged to that group. Otherwise the call stays on the caller’s own budget. See [Group Managers](gen3/groups/managers).

### Prices under one cent

A per-item rate under one cent, such as $0.008, keeps a third decimal place on billing amounts. A price of one cent or more still rounds to the nearest cent. Operators set those rates on [Model Pricing](gen3-admin/financial-controls/model-pricing).

## Related pages

- [Observability](gen3/observability)
- [Group Managers](gen3/groups/managers)
- [Model Pricing](gen3-admin/financial-controls/model-pricing)
