# Tenant Owner Guide

## Start Here

1. Open **Account Settings** from the account menu for tenant policy and recovery posture.
2. Use **Management → Users** for account lifecycle.
3. Review **Management → Observability** for tenant-wide analytics.
4. Browse **Management → Model Catalog** when you need deployment model inventory.
5. Coordinate support contacts via Control Panel **Email Settings** when published addresses are wrong.

## Why this matters

Owners hold tenant policy authority; misconfiguration here affects every user’s sign-in, recovery, and support experience.

## Details

`Tenant Owner` is the top tenant-app governance role in Gen 3. Owners can perform every tenant-manager workflow, plus the authority-bearing actions that remain intentionally restricted to owners.

## What a tenant owner adds

In addition to the delegated workflows described in the [Tenant Manager Guide](gen3/tenant-admin/tenant-managers), tenant owners can:

- assign and remove `Tenant Owner`
- assign and remove `Tenant Manager`
- manage elevated tenant accounts, not only standard tenant users
- edit owner-only tenant policy controls in [Account Settings](gen3/settings)
- operate with full tenant-wide visibility in [Observability](gen3/observability)

## Owner-first responsibilities

Use tenant-owner authority when the task changes who holds governance power inside the tenant app. Typical owner-only responsibilities include:

- deciding who becomes a manager or owner
- reviewing or correcting elevated-account posture
- approving tenant policy changes that affect recovery or support behavior
- resolving investigations that require unrestricted tenant-wide context

## Typical owner workflow

1. Confirm the operational issue on **Management → Users** or **Management → Observability**.
2. Decide whether the requested change affects authority boundaries, tenant-wide policy, or other elevated accounts.
3. Apply the role, policy, or remediation change.
4. Re-check observability or access state if the issue involved authentication, cost, or broad usage anomalies.

## Common tasks

### Promote or demote an elevated account

Use [Users](gen3/users) when you need to assign or remove `Tenant Manager` or `Tenant Owner`. This is owner-only because it changes who can govern the tenant, not just who can use the workspace.

### Edit tenant policy

Use [Account Settings](gen3/settings) when tenant policy text, password-reset posture, or account-recovery guidance must change. If the page is being used only to review policy, managers and users may still have read-only context, but only owners can save the tenant-governance changes.

### Investigate a tenant-wide incident

Use [Observability](gen3/observability) when an incident spans multiple users, groups, or billing signals and delegated scope is not enough. Owners should use the wider view sparingly and only when the investigation truly requires tenant-wide context.

### Correct elevated-account posture

Use [Users](gen3/users) to disable, re-enable, reset MFA, or otherwise correct elevated accounts when governance access itself is the issue. Document the reason for the change and coordinate with other owners when appropriate.

## Decision guide

Use owner authority when:

- the task changes who can govern the tenant app
- the target account is already elevated
- the fix requires tenant-wide policy or unrestricted tenant-wide evidence

Delegate to a tenant manager when:

- the work only affects standard tenant-user operations
- the issue is routine onboarding, MFA, or limited-scope support
- no tenant-policy or authority-boundary change is required

## Best practices

- Use owner authority only for tasks that truly require it.
- Avoid concentrating elevated access in more accounts than necessary.
- Pair sensitive changes with observability review when the issue touched authentication or misuse concerns.
- Keep managers empowered for delegated work, but do not blur the owner-only boundary.

## Related pages

- [Tenant Manager Guide](gen3/tenant-admin/tenant-managers)
- [Users](gen3/users)
- [Observability](gen3/observability)
- [Account Settings](gen3/settings)
