# Users

## Start Here

1. Confirm you are a **tenant owner** or **tenant manager**—both roles see **Users** in the tenant sidebar.
2. Open **Users** from the tenant sidebar.
3. Search for the account to create, edit, or disable.
4. Apply role changes through the edit panel and save.

## Why this matters

Tenant user administration stays in the tenant app so owners/managers can onboard teams without Control Panel credentials.

## Details

`Users` is the active Gen 3 tenant-account administration page. **Tenant owners and tenant managers** both see it in the sidebar and can manage tenant-app users (with different authority limits). It does not appear for tenant users.

## What the page supports

The current tenant `Users` page supports:

- browsing tenant accounts
- filtering by role and status
- searching by name, email, or tenant
- creating a new tenant account
- editing role, status, and onboarding details
- resetting MFA enrollment
- sending password-reset links
- resending welcome email
- bulk updates for selected users

## Roles you can manage

The tenant app currently recognizes three tenant roles:

- `Tenant Owner`
- `Tenant Manager`
- `Tenant User`

Tenant owners can manage the full tenant-role set. Tenant managers are intentionally limited to delegated user-management work and should expect tighter permissions when editing other accounts.

## Visibility and authority

- `Tenant Users` do not see this route in the current GT3 tenant navigation.
- `Tenant Managers` can work with standard tenant-user lifecycle tasks, but cannot create or assign elevated tenant roles.
- `Tenant Owners` can manage the full elevated-role set and can correct owner-level governance posture when needed.

## Main page workflow

1. Open `Users`.
2. Choose the account domain and role filters that match the user you need.
3. Use search when you know the user name or email.
4. Open the row actions or the add/edit shelf.
5. Apply the required role, status, MFA, or onboarding change.

## Common tasks

### Add a user

1. Select **Add User**.
2. Enter the email and optional name fields.
3. Choose the correct tenant role.
4. Confirm status and onboarding settings.
5. Save the new user.

Tenant managers should expect the role picker to be restricted to `Tenant User`. Tenant owners can assign the elevated tenant roles as well.

### Reset MFA enrollment

Use the user row action or a bulk action to reset MFA when a user has lost access to their authenticator and needs to enroll again at the next sign-in.

### Send a password reset

Use the row action when a user needs a fresh reset email. If reset email delivery fails, ask a Control Panel operator to review the deployment SMTP posture in `Email Settings`.

### Resend a welcome email

Use the row action when a new user did not receive onboarding email or when you intentionally want to restart that onboarding communication.

### Promote or demote a role

Use the edit shelf when a user needs a different tenant-account role. Promotions into `Tenant Manager` or `Tenant Owner` are owner-only actions, so escalate those requests when you are operating as a tenant manager.

## Relationship to other admin pages

- [Tenant Manager Guide](gen3/tenant-admin/tenant-managers) explains the delegated tasks a manager can perform from this page
- [Tenant Owner Guide](gen3/tenant-admin/tenant-owners) explains the elevated-account and role-assignment tasks that remain owner-only
- [Account Settings](gen3/settings) controls tenant policy, not user roster management
- [Groups](gen3/groups) controls collaboration membership and shared resources, not tenant account lifecycle
- [Observability](gen3/observability) uses these user identities for role-aware scope and analytics filters

## Best practices

- Assign the least-privileged role that still allows the user to do their job.
- Treat elevated-role assignment as a governance decision, not just an onboarding shortcut.
- Reset MFA only when a user truly needs re-enrollment.
- Use bulk actions carefully so you do not unintentionally affect the wrong account set after filtering.
- Confirm welcome email and password-reset delivery paths before assuming the user-management action failed.

## Related pages

- [Groups](gen3/groups)
- [Observability](gen3/observability)
- [Account Settings](gen3/settings)
- [Tenant Administration](gen3/tenant-admin)
