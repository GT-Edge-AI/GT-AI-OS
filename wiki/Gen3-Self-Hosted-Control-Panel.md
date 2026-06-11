# Self-Hosted Control Panel setup

First-time setup on the machine you installed. Assumes you completed an [install runbook](Gen3-Self-Hosted-Installation) and can open the Control Panel URL from that runbook.

---

## 1. Sign in and complete QuickStart

1. Open **Control Panel** at `https://<lan-ip>:3001/login` with the install default (`gtadmin@test.com` / `Test@123`) unless you already changed it.
2. Complete the **QuickStart** wizard (`/dashboard/quickstart`) — free-tier **Groq Cloud** and **NVIDIA NIM** API keys, optional local **Ollama**, platform default models, users, and SMTP. See [Control Panel QuickStart](Gen3-Admin-Quickstart).
3. Change default passwords for operator accounts before wider use (Control Panel **Users** and tenant **Users** as your role allows).
4. If you have an **Enterprise license** file, open **License**, upload it, and confirm status is **active** before enabling SSO, compliance, billing, or GT API features.

---

## 2. Models and platform defaults

QuickStart covers baseline inference providers and default model confirmation. After QuickStart:

1. Open **Models** to adjust inference endpoints or add paid providers.
2. Confirm deployment-wide defaults on **Default Models** match your policy.
3. For read-only model browsing tenants use later, they open **Management → Model Catalog** in the tenant app (documented in **Gen 3 Getting Started** inside Instructions).

---

## 3. Enable GT AI OS Instructions and GT Helper

The **same Gen 3 instructions corpus** published with GT AI OS powers:

- **GT AI OS Instructions** — full articles in the Control Panel **Instructions** drawer (sidebar book icon) and the tenant account menu
- **GT Helper** — **?** help shelf on the Control Panel shell and tenant UI (search, route suggestions, **Ask GT Helper**)

### Instructions Settings

1. In Control Panel, open **Instructions Settings** (see **Gen 3 Admin — Instructions Settings** in the Instructions drawer for field-level detail).
2. Configure optional **external documentation** links if your organization hosts additional browser docs.
3. Confirm the deployment can reach the instructions wiki source (default: published GT AI OS wiki content).

### GT Helper on Control Panel

1. Use the **?** bubble (lower-right on most operator pages).
2. Try **Search instructions** and **Suggested for this page** for the route you are on.
3. Use **Ask GT Helper** for conversational guidance grounded in operator wiki excerpts.

Full Helper behavior: open **Instructions** → **GT Helper (Control Panel)** (`Gen3-Admin-Instructions-Helper`).

---

## 4. Hand off to in-app documentation (operators)

You are done with **host** install runbooks when the cluster is healthy. Day-2 operator work happens **inside the product**:

| Step | Where |
|------|--------|
| Operator orientation | Control Panel → **Instructions** → **Gen 3 Admin Getting Started** |
| Route-aware help | **? GT Helper** on the page you are configuring |
| SSO, backup, compliance, financial controls | Instructions articles under **Gen 3 Admin** (same drawer) |
| In-app update UI | **Updates** dashboard — see **Gen 3 Admin — Updates** in Instructions |

Browser mirror (optional): [Gen 3 Admin Getting Started](Gen3-Admin-Getting-Started) on the GitHub wiki.

---

## 5. Hand off to tenant users

1. Share the tenant URL: `https://<lan-ip>:3002/login`.
2. Have users sign in (or provision accounts under **Users**).
3. Direct them to the account menu → **GT AI OS Instructions** → **Gen 3 Getting Started** for agents, chat, datasets, and teams.
4. Tenant **? GT Helper** works the same way as on the Control Panel, scoped to the tenant instructions corpus.

Browser mirror (optional): [Gen 3 Getting Started](Gen3-Getting-Started).

---

## 6. Optional enterprise features

After license activation, enable features as needed using Instructions articles:

- **SSO** — Gen 3 Admin SSO
- **Compliance mode** — Gen 3 Admin Compliance Mode
- **GT API** — enable for the tenant, then **Gen 3 GT API Overview** in tenant Instructions

---

## Host maintenance (not in Instructions)

| Task | Runbook |
|------|---------|
| Upgrade app version on the cluster | [Self-Hosted updating](Gen3-Self-Hosted-Updating) |
| Re-install from scratch | [Self-Hosted installation](Gen3-Self-Hosted-Installation) |

---

## Support

- **In-app:** **Contact support** when configured under Instructions Settings
- **Install/update issues on the host:** [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues)
- **Operator troubleshooting articles:** Control Panel **Instructions** (search or GT Helper), including super-admin troubleshooting topics where your role allows
