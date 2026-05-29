# Account Settings

## Start Here

1. Open **Account Settings** from the user account menu in the sidebar footer (click your name or profile icon, then **Settings** or **Profile**).
2. Review password-reset and account-recovery policy text.
3. If you are a **tenant owner**, update tenant policy and save.
4. Confirm support contact display; fix publishing in Control Panel **Email Settings** if incorrect.

## Why this matters

Account Settings holds tenant-facing policy that end users experience during recovery—not deployment branding owned by operators.

## Details

`Account Settings` is the active Gen 3 tenant policy page. It is not a duplicate of Control Panel settings. Instead, it holds the tenant-facing settings that belong inside the tenant app, while Control Panel operators still own deployment-wide branding, SMTP, and operator-security settings.

The route can still load for lower tenant roles when they need profile or policy context, but tenant owners hold the save authority for the owner-only tenant policy controls.

## What the page controls

The current page focuses on:

- tenant-facing profile and policy text
- password-reset policy for the tenant runtime
- account-recovery guidance
- read-only display of the published support contact policy

## What does not live here

These settings are managed elsewhere:

- deployment branding, operator MFA, session policy, and backup posture live in the Control Panel `Settings` page
- support email and support portal publishing live in the Control Panel `Email Settings` page
- tenant account administration lives in [Users](gen3/users)

## Common tasks

### Review tenant policy

Open this page when you need to confirm how the tenant wants password reset and account-recovery behavior handled.

### Update tenant policy

Tenant owners can update the tenant-level policy form and save the changes directly from this page. If the page loads but the form is effectively read-only to you, confirm whether your role is a tenant owner and whether the requested change belongs to the [Tenant Owner Guide](gen3/tenant-admin/tenant-owners) workflow rather than routine user support.

### Confirm support contact behavior

The page shows support-contact information as a read-only reflection of the Control Panel support policy. If the support address or support portal is wrong, fix it in the Control Panel `Email Settings` page, not here.

## Relationship to sign-in and recovery

Password reset and account recovery continue through the tenant sign-in experience. This page controls policy and communication, not the actual login screen workflow itself.

## Best practices

- Treat this page as tenant policy, not as a general user-profile editor.
- Use it to confirm what end users should expect from password reset behavior.
- Coordinate with Control Panel operators when support-contact details need to change.
- Route authority questions through [Tenant Administration](gen3/tenant-admin) before editing tenant-wide policy.

## Related pages

- [Support](gen3/getting-support)
- [Users](gen3/users)
- [Tenant Administration](gen3/tenant-admin)
