# Settings

## Start Here

1. Open **Settings** for deployment-wide operator policy.
2. Review session, MFA, branding, and object-storage controls; use [Backup & Restore](gen3-admin/backup-restore) for CNPG schedules and restore workflows.
3. Distinguish these from tenant [Account Settings](gen3/settings)—different plane.
4. Save changes during a maintenance window when sessions may reset.

## Why this matters

Operator settings affect every tenant’s hosting environment; tenant settings only affect tenant-facing policy inside the tenant app.

## Details

`Settings` is the Control Panel route for deployment-wide configuration that does not belong to a narrower admin page. It combines branding, operator MFA posture, session timeout policy, and reusable object storage configuration. CloudNativePG backup schedules, on-demand runs, and staged restore workflows live on [Backup & Restore](gen3-admin/backup-restore).

## Main sections

### Branding

Use this section to manage the deployment display name and branding assets surfaced across GT AI OS.

### Operator security

This section controls the Control Panel operator MFA posture. It is distinct from tenant-user MFA management on [Users](gen3-admin/users).

### Session timeout policy

Use this section to adjust the deployment-wide idle timeout applied across GT AI OS sessions.

### Object storage

This section defines reusable object-storage targets—S3-compatible bucket endpoints, path prefixes, and Kubernetes secret references—that backup and related deployment storage workflows consume. Configure object storage here before enabling CNPG backup automation on [Backup & Restore](gen3-admin/backup-restore).

## When to use Settings

Use this page when the change affects the deployment as a whole rather than one business function such as licensing, email, or model configuration.

## Recommended workflow

1. Change one configuration area at a time.
2. Save the update.
3. Verify the affected surface before moving to the next section.

This keeps it clear which deployment-wide setting caused an observed change.

## Best practices

- Treat branding and security changes as separate decisions.
- Review session timeout changes against evidence from [Access Logs](gen3-admin/access-logs).
- Confirm object-storage settings on this page before enabling or changing CNPG backup automation on [Backup & Restore](gen3-admin/backup-restore).
- Use the deployment display name deliberately because it appears across shared product surfaces.

## Related pages

- [Backup & Restore](gen3-admin/backup-restore)
- [Users](gen3-admin/users)
- [Access Logs](gen3-admin/access-logs)
- [Email Settings](gen3-admin/email-settings)
