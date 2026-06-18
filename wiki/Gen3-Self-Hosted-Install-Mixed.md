# Install — mixed ingress

Install GT AI OS when **Control Panel** and **Tenant App** need **different** ingress models — for example operators on **LAN** `https://<node-ip>:3001` while tenant users reach a **public** hostname via Cloudflare or NAT & DNS.

[← Back to installation hub](Gen3-Self-Hosted-Installation)

---

## Common mixed patterns

| Pattern | Control Panel | Tenant App | Typical use |
|---------|---------------|------------|-------------|
| **A — public tenant, private admin** | **1** LAN only | **3** Cloudflare tunnel | Internet tenant; admins on LAN only |
| **B — public tenant, private admin (NAT)** | **1** LAN only | **2** NAT & DNS hostname | Tenant on public FQDN without Cloudflare |
| **C — both public, different methods** | **2** NAT & DNS | **3** Cloudflare | Rare; pick per DNS/tunnel ownership |
| **D — full matrix** | Any **1–3** | Any **1–3** | See pairing table below |

If **any** app uses Cloudflare, complete **one** Cloudflare profile (**commercial** or **government**) for the whole install.

---

## Pairing matrix

| Control Panel \ Tenant | LAN (1) | NAT & DNS (2) | Cloudflare (3) |
|------------------------|---------|---------------|----------------|
| **LAN (1)** | ✓ [Local LAN](Gen3-Self-Hosted-Install-Local-LAN) | ✓ | ✓ (pattern A / B) |
| **NAT & DNS (2)** | ✓ | ✓ [NAT & DNS](Gen3-Self-Hosted-Install-NAT-DNS) | ✓ |
| **Cloudflare (3)** | ✓ | ✓ | ✓ [Cloudflare](Gen3-Self-Hosted-Install-Cloudflare) |

**Local Portable (4)** applies to both apps together — see [Install — Local Portable](Gen3-Self-Hosted-Install-Local-Portable).

---

## Prerequisites

Combine prerequisites from each app’s model:

- **LAN:** static node IP (or autodetect for mixed LAN admin)
- **NAT & DNS:** public FQDNs + firewall **443 → :3001 / :3002** — see [Install — NAT & DNS](Gen3-Self-Hosted-Install-NAT-DNS#prerequisites)
- **Cloudflare:** API token, account ID, hostnames — see [Install — Cloudflare](Gen3-Self-Hosted-Install-Cloudflare#1-cloudflare-api-token-and-account-id)
- [Shared prerequisites](Gen3-Self-Hosted-Installation#shared-prerequisites)

---

## 1. Install the Quick Installer

```bash
TAG="$(curl -fsSL https://api.github.com/repos/GT-Edge-AI/GT-AI-OS/releases/latest | grep '"tag_name"' | head -1 | cut -d'"' -f4)"
VER="${TAG#v}"
curl -fsSL -o /tmp/gt-ai-os.deb \
  "https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/${TAG}/GT-AI-OS-Quick-Installer_${VER}_all.deb"
sudo apt install -y /tmp/gt-ai-os.deb
sudo -E gt-ai-os-operator
```

---

## 2. Operator menu

| When you see | Choose |
|--------------|--------|
| **What do you want to do?** | **1** (Install) |
| **Install — choose style** | **1** (Interactive) |

---

## 3. Install wizard — pattern A (LAN Control Panel, Cloudflare Tenant)

Complete the [shared wizard steps](Gen3-Self-Hosted-Installation#shared-wizard-steps-every-scenario), then:

| When you see | Choose or enter |
|--------------|-----------------|
| **Control Panel — access model** | **1** (LAN only) |
| **Tenant App — access model** | **3** (Cloudflare tunnel) |
| **Cloudflare profile** | **1** (commercial) or **2** (government) |
| **Control Panel LAN host** | Node LAN IP (for example `192.168.1.50`) |
| **Tenant app public hostname** | FQDN only (for example `app.example.com`) |
| **Cloudflare API token / account ID** | When prompted after install confirmation |

The install enables **tenant-only network access** when the Control Panel stays on LAN and the tenant is public.

---

## 4. Install wizard — pattern B (LAN Control Panel, NAT & DNS Tenant)

| When you see | Choose or enter |
|--------------|-----------------|
| **Control Panel — access model** | **1** (LAN only) |
| **Tenant App — access model** | **2** (NAT & DNS hostname) |
| **Control Panel LAN host** | Node LAN IP |
| **Tenant App LAN host** | Node LAN IP (for `:3002` on LAN) |
| **Tenant public NAT/DNS hostname** | FQDN (for example `tenant.example.com`) |

Ensure firewall **443 → 3002** and your public DNS A record are in place before external users test.

---

## 5. Log in

Use the URL that matches each audience:

| Audience | Control Panel | Tenant app |
|----------|---------------|------------|
| **LAN operators** (pattern A or B) | `https://<lan-ip>:3001/login` | `https://<lan-ip>:3002/login` (if tenant is LAN-only) |
| **Internet users** (Cloudflare tenant) | — | `https://<tenant-fqdn>/login` |
| **Internet users** (NAT tenant) | — | `https://<tenant-fqdn>/login` |

Confirm deployed URLs:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin report --namespace <your-namespace>
```

---

## Next step

[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)
