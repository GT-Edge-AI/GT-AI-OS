# Tenant Administration

## Start Here

1. Confirm your role is **tenant manager** or **tenant owner**.
2. Open governance pages from the sidebar: **Management → Users** or **Management → Observability** as your role allows.
3. Open **Account Settings** or **Profile** from the account menu for tenant policy (owners) or read-only policy context.
4. Choose the guide that matches your role ([Tenant Manager](gen3/tenant-admin/tenant-managers) vs [Tenant Owner](gen3/tenant-admin/tenant-owners)).
5. Coordinate with Control Panel operators for deployment-wide policy.

## Why this matters

Tenant administration articles separate manager vs owner duties so policy changes are deliberate and auditable.

## Details

`Tenant Administration` is the role-specific guidance shelf for the active Gen 3 tenant governance surfaces. It does not introduce a separate hidden application. Instead, it explains how the live **Management → Users**, **Management → Observability**, **Management → Model Catalog**, and account-menu **Settings** pages behave for elevated tenant roles.

## Who should use this section

- `Tenant Managers` use this section when they need delegated tenant operations without full owner authority.
- `Tenant Owners` use this section when they need full tenant-app governance, including owner-only policy and role decisions.
- `Tenant Users` do not see this section because the underlying governance routes are hidden from standard tenant-user sessions.

## What lives here

- [Tenant Manager Guide](gen3/tenant-admin/tenant-managers) explains the delegated governance work that managers can perform in the live tenant app.
- [Tenant Owner Guide](gen3/tenant-admin/tenant-owners) explains the additional controls that remain owner-only in the live tenant app.

## Related live pages

- [Users](gen3/users) — **Management → Users** (tenant owners and managers).
- [Observability](gen3/observability) — **Management → Observability** (all signed-in roles; tabs vary).
- [Model Catalog](gen3/model-catalog) — **Management → Model Catalog** (all signed-in roles).
- [Account Settings](gen3/settings) — account menu **Settings** / **Profile**; owner-only policy editing.
- [GT API](gen3/gt-api/overview) — top-level sidebar when `gtApiEnabled` (not under Management).

## Operating principle

Keep governance work separate from day-to-day end-user workflows. If a task changes tenant-account roles, status, MFA posture, investigation scope, or tenant policy, use this section to confirm whether it belongs to a tenant manager or a tenant owner before you act.
