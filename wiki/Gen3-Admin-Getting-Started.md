# Control Panel Getting Started

## Start Here

- To get the GT AI OS Control Panel Quick Start Manual for your version of GT AI OS, [go here](https://drive.google.com/drive/folders/1LxpupHdrbs63OfGceQMo8rggnsluqFH6?usp=drive_link).
- Ensure you select the manual for your currently deployed version of GT AI OS.
- Feel free to browse any version manual as you wish.

1. Sign in to the **Control Panel** operator UI.
2. Open **Dashboard** for deployment health summary.
3. Review [Models](gen3-admin/models) before tenants consume new providers.
4. Configure [Email Settings](gen3-admin/email-settings) and [Instructions Settings](gen3-admin/instructions-settings) for tenant-facing behavior.
5. Use the **?** help shelf ([GT Helper](gen3-admin/instructions-helper)) on the Control Panel shell for operator instructions search and **Ask helper** chat.

![Control Panel Help shelf](gen3-admin/images/cp-help-shelf.png)

## Why this matters

Control Panel operators own deployment-wide integration, policy, and observability—distinct from tenant self-service workspaces.

## Details

The Gen 3 Control Panel is the operator workspace for deployment-wide administration. These pages are distinct from the tenant app and focus on runtime posture, identity, model integration, licensing, billing controls, and deployment configuration.

## Active Control Panel workspaces

| Workspace | What it currently controls |
| --- | --- |
| [Dashboard](gen3-admin/dashboard) | deployment summary and quick jump points |
| [Users](gen3-admin/users) | operator and tenant-app account administration |
| [SSO Providers](gen3-admin/sso) | upstream OIDC or SAML providers plus provisioning policy |
| [Models](gen3-admin/models) | inference providers, configured models, and default model selections |
| [Updates](gen3-admin/updates) | immutable release update requests, approval, rollback, and progress monitoring |
| [Backup & Restore](gen3-admin/backup-restore) | CNPG backup schedules, on-demand runs, and staged database restore workflows |
| [Financial Controls](gen3-admin/financial-controls) | billing enablement, pricing, allocations, and budget policy |
| [Email Settings](gen3-admin/email-settings) | SMTP transport, support policy, welcome-email controls, and broadcast send/review |
| [Email Templates & Modules](gen3-admin/email-templates) | welcome, password-reset, broadcast template authoring and reusable header/footer modules |
| [License](gen3-admin/licenses) | license status, deployment identifier, and activation |
| [Access Logs](gen3-admin/access-logs) | sign-in and session-event review |
| [CTP Helper Usage](gen3-admin/helper-usage) | Control Panel ? help-shelf thread and token observability |
| [Compliance Mode](gen3-admin/compliance-mode) | deployment-wide compliance copy and notice posture |
| [Instructions Settings](gen3-admin/instructions-settings) | optional external instructions link exposed in both apps |
| [GT Helper](gen3-admin/instructions-helper) | Control Panel **?** help shelf — wiki search, page suggestions, and **Ask helper** chat |
| [Settings](gen3-admin/settings) | deployment branding, operator security, session policy, and object storage targets |

## Recommended first operator walkthrough

1. Open [Dashboard](gen3-admin/dashboard) to confirm license and user posture.
2. Review [Users](gen3-admin/users) to confirm the account mix and MFA state.
3. Check [Models](gen3-admin/models) if the deployment depends on external inference providers.
4. Confirm [Email Settings](gen3-admin/email-settings) and [License](gen3-admin/licenses) before onboarding users.
5. Use [Settings](gen3-admin/settings) for deployment-wide posture such as branding and session timeout, then [Backup & Restore](gen3-admin/backup-restore) for CNPG schedules and restore drills.

## Important route boundaries

- `Models` now absorbs the provider and API-key workflows; the legacy `providers` and `api-keys` URLs are redirect shims into the models page.
- `Financial Controls` is for pricing and billing policy, not the place to activate a license.
- `Settings` is for deployment-level configuration, while tenant policy lives in the tenant app `Account Settings` page.

## Migration note

Gen 2 operator docs remain live in parallel. Gen 3 Control Panel pages are namespaced under `gen3-admin/...` so the active Gen 3 operator shell can be documented without disturbing the still-supported Gen 2 corpus.
