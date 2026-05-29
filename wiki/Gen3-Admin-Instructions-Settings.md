# Instructions Settings

## Start Here

1. Open **Instructions Settings**.
2. Decide whether to enable the optional external documentation link (label, URL, and enable toggle).
3. Save and confirm the tenant user account menu and Control Panel shell show the expected external link when enabled.
4. Test tenant and Control Panel Instructions drawers after changes.

![Control Panel Help shelf with search, suggestions, and Ask helper](gen3-admin/images/cp-help-shelf.png)

## Why this matters

Instructions Settings wires deployments to the wiki corpus tenants see in-app—stale URLs break the help experience.

## Details

`Instructions Settings` manages the optional external documentation link that can appear alongside the built-in GT AI OS instructions experience in both the tenant app and the Control Panel.

## What this page does

The page controls:

- whether the external documentation button is shown
- the label displayed to users
- the target URL

## What this page does not do

This page does not author or edit the built-in markdown instructions corpus. The built-in instructions are repo-backed and loaded through the dedicated Gen 3 wiki indexes for tenant and Control Panel drawers.

The built-in **Instructions** drawer holds stable articles and screenshots. The fixed **?** help shelf ([GT Helper](gen3-admin/instructions-helper)) complements it with route-aware suggestions and conversational **Ask helper** chat grounded in the same wiki corpus.

## Publishing workflow

1. Decide whether you want an external docs link at all.
2. Enable the external link.
3. Enter the user-facing label.
4. Enter the URL.
5. Save the change.
6. Confirm the tenant and Control Panel drawers show the expected button and destination.

## When to use this feature

Use the external link when your deployment has additional operator or customer documentation that should sit next to, not replace, the built-in in-product instructions.

## Best practices

- Keep the label simple so users know the link leaves the built-in instructions.
- Point to stable documentation URLs rather than temporary review links.
- Remember that disabling the link does not affect the built-in repo-backed instructions corpus.

## Related pages

- [GT Helper](gen3-admin/instructions-helper)
- [Email Settings](gen3-admin/email-settings)
