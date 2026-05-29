# Users

## Start Here

1. Open **Users** in the Control Panel.
2. Locate operator or service accounts to adjust.
3. Apply MFA and role policy per deployment standards.
4. Avoid using tenant-app **Users** for operator identities—they are separate planes.

## Why this matters

Control Panel users are operator accounts with a different trust boundary than tenant end users.

## Details

The Control Panel `Users` page is the deployment-wide identity workspace. It manages both Control Panel operator accounts and tenant-app accounts from one route, with filters that let you move between those two populations without leaving the page.

## What the page currently supports

- viewing all accounts or switching to Control Panel-only or tenant-app-only views
- filtering by role and status
- searching by name, email, or tenant
- creating and editing users
- enabling or disabling accounts
- resetting MFA enrollment
- sending password resets
- resending welcome email
- importing users in bulk
- applying bulk actions to selected accounts

## Account domains

The page separates accounts into three operator-friendly views:

- `All accounts`
- `Control Panel accounts`
- `Tenant accounts`

Use those first before applying role or status filters.

## Roles you will see

The exact options depend on the selected account domain, but the current Gen 3 implementation distinguishes Control Panel operator roles such as super admin and environment admin from tenant-app roles such as tenant owner, tenant manager, and tenant user.

## Common tasks

### Add a new account

1. Open `Users`.
2. Choose the correct account domain first.
3. Select **Add User**.
4. Enter identity details.
5. Choose the role and status.
6. Save the account.

### Reset MFA enrollment

Use the row action or bulk action when a user must re-enroll MFA at the next sign-in.

### Disable an account

Disable when access should stop without deleting the historical identity record.

### Import users

Use bulk import when onboarding a prepared list of accounts. Make sure the CSV or pasted rows match the intended account domain so Control Panel-only roles are not imported through a tenant-only view.

## Best practices

- Pick the correct account domain before you create or import users.
- Assign the minimum role needed.
- Use disable before delete when you may need to preserve the account record.
- Check MFA posture before troubleshooting login issues elsewhere.

## Related pages

- [Access Logs](gen3-admin/access-logs)
- [Email Settings](gen3-admin/email-settings)
- [Settings](gen3-admin/settings)
