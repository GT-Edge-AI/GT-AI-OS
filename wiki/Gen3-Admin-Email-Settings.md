# Email Settings

## Start Here

1. Open **Email Settings**.
2. Configure SMTP or provider credentials for transactional email.
3. Publish tenant support email and portal links tenants see read-only in Account Settings.
4. Send a test message after credential changes.

## Why this matters

Tenants display support contacts from this policy; wrong values generate support noise in the tenant app.

## Details

`Email Settings` is the active Gen 3 Control Panel route for outbound email and tenant-visible support policy. It combines SMTP transport, support-contact publishing, welcome-email controls, and broadcast compose/send/review.

**Email Templates & Modules** is a separate sidebar route documented at [Email Templates & Modules](gen3-admin/email-templates). Use that page when you need to create, edit, preview, or delete template bodies and shared modules—not when you are only configuring SMTP or sending a broadcast from Email Settings.

## What the page currently supports

- configuring SMTP host, port, credentials, and TLS posture
- publishing tenant-visible support email and support portal values
- enabling or disabling welcome email behavior
- editing welcome-email copy fields
- selecting welcome and password-reset templates for live email flows
- composing, previewing, sending, and reviewing broadcast records

## Main sections

### SMTP Configuration

This is the transport layer. If password resets or welcome emails are not being delivered, start here first.

### Support contact policy

This section controls what tenant users see under **Contact support**. It can publish email-only, portal-only, or combined support paths.

### Welcome email policy

Use this section to control whether onboarding email is sent and what subject/body content should be used.

### Broadcasts

Use the broadcast tab to compose audience-targeted messages, attach an existing broadcast template, include optional modules, preview recipients, and send or review broadcast records.

Template and module **authoring** lives on the separate **Email Templates & Modules** sidebar route. Email Settings consumes those artifacts when you pick templates for welcome, password-reset, or broadcast flows.

## Recommended workflow

1. Confirm SMTP works.
2. Publish the correct support contact policy.
3. Review welcome-email behavior.
4. Confirm templates and broadcasts reflect the intended deployment communications.

## Troubleshooting sequence

If a user reports missing email:

1. Check SMTP configuration.
2. Confirm the welcome-email or password-reset path is actually enabled.
3. Confirm the support policy points to the right contact path.
4. Return to [Users](gen3-admin/users) if the underlying user action needs to be re-sent.

## Best practices

- Keep support email and support portal details accurate because they surface directly in the tenant shell.
- Treat SMTP transport and support-contact policy as separate concerns.
- Re-test or re-validate user onboarding after major welcome-email changes.

## Related pages

- [Email Templates & Modules](gen3-admin/email-templates)
- [Users](gen3-admin/users)
- [Instructions Settings](gen3-admin/instructions-settings)
