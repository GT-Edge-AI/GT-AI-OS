# Email Templates & Modules

## Start Here

1. Open **Email Templates & Modules** from the Control Panel sidebar.
2. Choose a template tab (**Welcome Templates**, **Password Reset Templates**, or **Broadcast Templates**) to author or edit message bodies.
3. Switch to **Modules** when you need reusable header or footer snippets shared across templates.
4. Use **Preview** before promoting a template to **Default** for its type.
5. Return to [Email Settings](gen3-admin/email-settings) to configure SMTP, pick active templates for welcome/password-reset flows, or send broadcasts.

## Why this matters

This page owns reusable email **content**. [Email Settings](gen3-admin/email-settings) owns transport (SMTP), support-contact publishing, and selecting which template to send—keeping authoring separate from delivery reduces accidental production sends while editing copy.

## Details

`Email Templates & Modules` is the active Gen 3 Control Panel route at `/dashboard/email-templates`. The page header describes managing welcome, password reset, and broadcast templates plus reusable header and footer modules.

## The four tabs

| Tab | Template type | Purpose |
| --- | --- | --- |
| Welcome Templates | `welcome` | Onboarding email bodies consumed when welcome email is enabled on Email Settings |
| Password Reset Templates | `password_reset` | Password-reset message bodies selected on Email Settings |
| Broadcast Templates | `broadcast` | Reusable broadcast bodies reviewed or sent from Email Settings |
| Modules | — | Shared header/footer snippets attached to individual templates |

Each template tab lists cards for templates of that type. The **Modules** tab lists reusable modules separately.

## Template cards

Each template card shows:

- name and optional description
- **Default** badge when the template is the default for its type
- **Inactive** badge when `isActive` is false
- module count badge
- subject line and truncated body preview
- last updated timestamp

### Template actions (overflow menu and footer)

| Action | Purpose |
| --- | --- |
| Preview | Render a sanitized HTML preview in a dialog |
| Edit | Open the template editor dialog |
| Duplicate | Create a copy with `(Copy)` appended to the name (not default) |
| Make default | Promote the template as the default for its type (disabled for read-only operators) |
| Delete | Remove a non-default template |

Default templates cannot be deleted from the overflow menu.

## Template editor dialog

Creating or editing a template requires:

- **Name**
- **Subject**
- **Body** (rich-text HTML via the email editor)

Optional fields include description and active/default flags. Templates can attach **module IDs** so shared header/footer modules render inside the final message.

Save creates or updates through the Control Panel email-template API. Read-only operator sessions cannot save changes.

## Modules tab

Modules are reusable snippets with:

- name and description
- **Position** — `header` or `footer`
- **Auto include** — when enabled, the module can be applied automatically according to module rules
- **Sort order** — ordering among modules
- **Active** state

Module actions mirror templates: create, edit, duplicate, delete (via overflow menu), with card previews showing truncated content.

Use modules to keep legal footers, branding headers, or repeated disclaimers consistent across welcome, password-reset, and broadcast templates.

## Relationship to Email Settings

| Task | Where to work |
| --- | --- |
| Author welcome/password-reset/broadcast HTML | **Email Templates & Modules** (this page) |
| Configure SMTP host, credentials, TLS | [Email Settings](gen3-admin/email-settings) |
| Enable welcome email and pick which welcome template sends | [Email Settings](gen3-admin/email-settings) |
| Publish tenant support email / portal | [Email Settings](gen3-admin/email-settings) |
| Send or review a broadcast using a broadcast template | [Email Settings](gen3-admin/email-settings) |

Tenant users see published support contacts read-only in tenant [Account Settings](gen3/settings); they do not edit templates here.

## Recommended workflow

1. Create or update modules for shared header/footer content.
2. Author template bodies on the appropriate tab and attach modules where needed.
3. Preview each template before promoting it.
4. Set **Make default** for the template that should become the type default.
5. Switch to [Email Settings](gen3-admin/email-settings) to wire SMTP and select templates for live flows.
6. Send a test message from Email Settings after credential or template changes.

## Best practices

- Keep one clear default template per type (welcome, password_reset, broadcast).
- Deactivate rather than delete when retiring copy you may need again.
- Use modules instead of duplicating footer legal text across many templates.
- Coordinate template placeholder changes with welcome-email policy on Email Settings.

## Related pages

- [Email Settings](gen3-admin/email-settings)
- [Users](gen3-admin/users)
- [Settings](gen3-admin/settings)
