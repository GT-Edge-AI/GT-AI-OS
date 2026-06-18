# Install — Cloudflare

Install GT AI OS on a single host so **internet** users reach Control Panel and the tenant app on **public hostnames** through a **Cloudflare Tunnel**.

[← Back to installation hub](Gen3-Self-Hosted-Installation)

---

## Prerequisites

- **Cloudflare account** with DNS zones for your two public hostnames
- **Cloudflare API token** and **account ID** (create and test in [section 1](#1-cloudflare-api-token-and-account-id) below)
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases), **`ghcr.io/gt-edge-ai`**, and **Cloudflare**
- [Shared prerequisites](Gen3-Self-Hosted-Installation#shared-prerequisites)

---

## 1. Cloudflare API token and account ID

Complete this section on any machine with a browser (or on the install host) before you run the operator.

### 1.1 Create the API token

1. Log in to the [Cloudflare dashboard](https://dash.cloudflare.com/).
2. Open **My Profile** → **API Tokens**.
3. Click **Create Token** → **Create Custom Token**.
4. Name the token (for example `gt-ai-os-commercial`).
5. Add permissions:
   - **Account** → **Cloudflare Tunnel** → **Edit**
   - **Zone** → **Zone** → **Read**
   - **Zone** → **DNS** → **Edit**
6. Under **Account Resources**, include the account that will own the tunnel.
7. Under **Zone Resources**, include the zones for your Control Panel and tenant hostnames.
8. Create the token and copy it once (Cloudflare will not show it again).

For **government** Cloudflare, use your government account and zones only. Do not reuse commercial tokens or account IDs.

### 1.2 Find the account ID

1. In the same Cloudflare account, open **any** DNS zone you will use.
2. On the zone **Overview** page, find **Account ID** in the API box (right side).
3. Copy that value. It is the **account** ID, not a zone ID.

### 1.3 Test token and account ID

```bash
export CLOUDFLARE_API_TOKEN="<your-api-token>"
export CLOUDFLARE_ACCOUNT_ID="<your-account-id>"

curl -fsSL \
  -H "Authorization: Bearer ${CLOUDFLARE_API_TOKEN}" \
  "https://api.cloudflare.com/client/v4/accounts/${CLOUDFLARE_ACCOUNT_ID}" \
  | python3 -m json.tool
```

**Good:** JSON with `"success": true`.

If that fails, list accounts the token can access:

```bash
curl -fsSL \
  -H "Authorization: Bearer ${CLOUDFLARE_API_TOKEN}" \
  "https://api.cloudflare.com/client/v4/accounts" \
  | python3 -m json.tool
```

Use the `id` from the correct account in the install wizard.

---

## 2. Install the Quick Installer

To pin a release, set `TAG` before download (for example `TAG=v3.0.4`). The `.deb` filename uses semver **without** the `v` prefix (`3.0.4` for tag `v3.0.4`).

```bash
TAG="$(curl -fsSL https://api.github.com/repos/GT-Edge-AI/GT-AI-OS/releases/latest | grep '"tag_name"' | head -1 | cut -d'"' -f4)"
VER="${TAG#v}"
curl -fsSL -o /tmp/gt-ai-os.deb \
  "https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/${TAG}/GT-AI-OS-Quick-Installer_${VER}_all.deb"
sudo apt install -y /tmp/gt-ai-os.deb
sudo -E gt-ai-os-operator
```

---

## 3. Operator menu

When the operator menu appears, choose the following:

| When you see | Choose |
|--------------|--------|
| **What do you want to do?** | **1** (Install) |
| **Install — choose style** | **1** (Interactive) |

---

## 4. Install wizard

Complete the [shared wizard steps](Gen3-Self-Hosted-Installation#shared-wizard-steps-every-scenario), then use these **ingress-specific** answers:

| When you see | Choose or enter |
|--------------|-----------------|
| **Control Panel — access model** | **3** (Cloudflare tunnel) |
| **Tenant App — access model** | **3** (Cloudflare tunnel) |
| **Cloudflare profile** | **1** (commercial) or **2** (government) — pick **one** account type only |
| **Control Panel public hostname** | FQDN only (for example `ctp.example.com`) |
| **Tenant app public hostname** | FQDN only (for example `app.example.com`) |
| **Cloudflare API token** (after you confirm install) | Token from [section 1.1](#11-create-the-api-token) |
| **Cloudflare account ID** | ID from [section 1.2](#12-find-the-account-id) |

After your last answer above, the install runs automatically. Expect **about 15 minutes** before the wizard finishes. Do not interrupt the terminal.

Save the **bootstrap Control Panel email** and **password** printed when the install finishes.

---

## 5. Log in to Control Panel

1. Open `https://<control-panel-hostname>/login` (the Control Panel hostname from the wizard).
2. Sign in with the bootstrap **email** and **password** from step 4.

To print bootstrap credentials again:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin bootstrap-creds --namespace <your-namespace>
```

Tenant app URL: `https://<tenant-hostname>/login`

---

## Next step

[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)
