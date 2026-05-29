# Tenant Manager Guide

## Start Here

1. Review your tenant manager scope on **Management → Users** and **Management → Groups**.
2. Use **Management → Observability** for managed-group or personal analytics as exposed to your role.
3. Escalate owner-only policy changes to a tenant owner via **Account Settings** (account menu).

## Why this matters

Managers run day-to-day onboarding and collaboration; this guide keeps their authority distinct from owner-only policy.

## Details

`Tenant Manager` is the delegated tenant-governance role in Gen 3. Managers can open **Management → Users** and **Management → Observability**, but they do not have the same authority as a tenant owner.

## What a tenant manager can do

In the current Gen 3 tenant app, a tenant manager can:

- open **Management → Users**
- create and manage `Tenant User` accounts
- reset MFA and password-help flows for eligible tenant users
- review tenant observability and billing analytics within the manager's effective scope
- manage managed-group governance and delegated operational work

## What stays owner-only

Tenant managers cannot perform the highest-impact tenant-governance actions. In practice that means:

- they cannot assign or promote `Tenant Owner`
- they cannot assign `Tenant Manager`
- they cannot manage owner accounts
- they cannot edit owner-only tenant policy controls in [Account Settings](gen3/settings)

If a task touches authority boundaries rather than routine operations, escalate it to a tenant owner instead of working around the restriction.

## Typical operating workflow

1. Start on **Management → Users** when the issue is account lifecycle, onboarding, MFA, or role review.
2. Move to **Management → Observability** when you need evidence about access patterns, usage, conversations, or billing posture.
3. Return to the affected account, group, or shared resource only after you know whether the problem is user-specific or tenant-wide.

## Common tasks

### Add a standard tenant user

Use [Users](gen3/users) to create `Tenant User` accounts for new staff or operators. Confirm the account role before saving, because managers are intentionally limited to the standard tenant-user role.

### Reset MFA or onboarding

Use the row actions on [Users](gen3/users) when a delegated tenant user loses their authenticator, misses a welcome email, or needs a new password-reset path. If the problem is delivery-related rather than account-related, ask a Control Panel operator to review deployment email posture.

### Investigate tenant activity

Use [Observability](gen3/observability) to review usage, conversations, access logs, and billing analytics within your scope. This is the right first step when a report sounds like misuse, unexpected cost growth, or a login issue.

### Govern managed groups

Use the live `Groups` workspace for managed-group membership and resource governance. Tenant-administration guidance belongs here when you are deciding whether a task is within manager authority; the actual group changes still happen in [Groups](gen3/groups).

## Decision guide

Use a tenant manager workflow when:

- the user being managed is a `Tenant User`
- the change is operational and reversible
- the issue can be resolved without altering tenant-wide authority boundaries

Escalate to a tenant owner when:

- the target account is already a manager or owner
- the requested role change would create or remove elevated authority
- the task requires tenant policy changes rather than account operations

## Best practices

- Treat delegated authority as a guardrail, not as a limitation to bypass.
- Use observability evidence before making broad user or governance changes.
- Keep account-role decisions aligned with least privilege.
- Escalate early when a request crosses into owner-only territory.

## Related pages

- [Users](gen3/users)
- [Observability](gen3/observability)
- [Groups](gen3/groups)
- [Tenant Owner Guide](gen3/tenant-admin/tenant-owners)
