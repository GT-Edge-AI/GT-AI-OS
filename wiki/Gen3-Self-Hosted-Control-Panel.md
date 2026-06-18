# Self-Hosted Control Panel setup

First-time setup on the machine you installed. Assumes you completed an [install runbook](Gen3-Self-Hosted-Installation) and can open the Control Panel URL from that runbook.

## Start Here

1. Sign in at the Control Panel URL from your install runbook and change default passwords before wider use.
2. Open **Models** and set deployment-wide defaults (including **Default GT Helper model** when you want **?** shelf chat).
3. Open **Instructions** (sidebar book icon) for operator articles, or use the **?** GT Helper shelf for chat-only guidance on the page you are configuring.
4. Share the tenant URL and point users to **GT AI OS Instructions** → [Getting Started](gen3/getting-started).

## Why this matters

Host install runbooks get the cluster healthy; this page bridges first login to day-2 operator and tenant onboarding inside the product. GT AI OS Instructions and GT Helper keep setup guidance in-app instead of scattered host notes.

## Details

### 1. Sign in and secure the deployment

1. Open **Control Panel** at `https://<lan-ip>:3001/login` with the install default (`gtadmin@test.com` / `Test@123`) unless you already changed it.
2. Change default passwords for operator accounts before wider use (Control Panel **Users** and tenant **Users** as your role allows).
3. If you have an **Enterprise license** file, open **License**, upload it, and confirm status is **active** before enabling SSO, compliance, billing, or GT API features.

### 2. Models and platform defaults

1. Open [Models](gen3-admin/models) (or **Default models / web search** per your build) and confirm inference endpoints match your environment.
2. Set **Default GT Helper model** so tenant and Control Panel **?** shelves can answer chat questions.
3. Set other defaults tenants will inherit where the UI exposes deployment-wide policy.
4. For read-only model browsing tenants use later, they open **Management → Model Catalog** in the tenant app (documented in [Getting Started](gen3/getting-started) inside Instructions).

### 3. Enable GT AI OS Instructions and GT Helper

The **same Gen 3 instructions corpus** published with GT AI OS powers:

- **GT AI OS Instructions** — full articles in the Control Panel **Instructions** drawer (sidebar book icon) and the tenant account menu
- **GT Helper** — **?** help shelf on the Control Panel shell and tenant UI (multi-turn chat only)

#### Instructions Settings

1. In Control Panel, open [Instructions Settings](gen3-admin/instructions-settings).
2. Configure optional **external documentation** links if your organization hosts additional browser docs.
3. Confirm the deployment can reach the instructions wiki source (default: published GT AI OS wiki content).

#### GT Helper on Control Panel

1. Use the **?** bubble (lower-right on most operator pages).
2. Ask substantive questions in the **GT Helper** chat pane; use **New question** and the thread rail for follow-ups.
3. Toggle **Float** / **Split** to dock the shelf beside page content on wide screens.
4. Open **Full instructions** or the sidebar **Instructions** drawer when you need wiki search, tree navigation, or long-form articles—the help shelf does not include search or page suggestions.

Full operator help shelf behavior: [GT Helper (Control Panel)](gen3-admin/instructions-helper).

Tenant users: [How to use GT Helper](gen3/gt-helper/overview).

### 4. Hand off to in-app documentation (operators)

You are done with **host** install runbooks when the cluster is healthy. Day-2 operator work happens **inside the product**:

| Step | Where |
|------|--------|
| Operator orientation | Control Panel → **Instructions** → [Admin Getting Started](gen3-admin/getting-started) |
| Route-aware help | **? GT Helper** chat on the page you are configuring |
| SSO, backup, compliance, financial controls | Instructions articles under **Gen 3 Admin** (same drawer) |
| In-app update UI | **Updates** dashboard — see [Updates](gen3-admin/updates) in Instructions (under development in interim builds) |

Browser mirror (optional): [Admin Getting Started](Gen3-Admin-Getting-Started) on the GitHub wiki.

### 5. Hand off to tenant users

1. Share the tenant URL: `https://<lan-ip>:3002/login`.
2. Have users sign in (or provision accounts under **Users**).
3. Direct them to the account menu → **GT AI OS Instructions** → [Getting Started](gen3/getting-started) for agents, chat, datasets, and teams.
4. Tenant **? GT Helper** works the same way as on the Control Panel—chat-only on the **?** shelf, with full wiki browse in **GT AI OS Instructions**.

Browser mirror (optional): [Getting Started](Gen3-Getting-Started).

### 6. Optional enterprise features

After license activation, enable features as needed using Instructions articles:

- **SSO** — [SSO](gen3-admin/sso)
- **Compliance mode** — [Compliance Mode](gen3-admin/compliance-mode)
- **GT API** — enable for the tenant, then [GT API Overview](gen3/gt-api/overview) in tenant Instructions

### Host maintenance (not in Instructions)

| Task | Runbook |
|------|---------|
| Upgrade app version on the cluster | [Self-Hosted updating](Gen3-Self-Hosted-Updating) |
| Re-install from scratch | [Self-Hosted installation](Gen3-Self-Hosted-Installation) |

### Support

- **In-app:** **Contact support** when configured under [Instructions Settings](gen3-admin/instructions-settings)
- **Install/update issues on the host:** [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues)
- **Operator troubleshooting articles:** Control Panel **Instructions** or **? GT Helper** chat, including super-admin troubleshooting topics where your role allows
