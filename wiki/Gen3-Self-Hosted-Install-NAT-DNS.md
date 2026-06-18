# Install — NAT & DNS

Install GT AI OS so **open-internet** users reach Control Panel and the tenant app on **portless public hostnames** (`https://<fqdn>`) via **DNS A records** and **firewall NAT** (public **443** → node **:3001** / **:3002**). This is **not** Cloudflare Tunnel.

LAN operators can still browse `https://<node-ip>:3001` and `:3002` directly.

[← Back to installation hub](Gen3-Self-Hosted-Installation)

---

## Prerequisites

- Static **LAN IP** for the install node
- Two **public DNS hostnames** (Control Panel and Tenant) with A records to your public IP
- Firewall rules: public **443** → node **3001** (Control Panel) and **3002** (Tenant)
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`**
- [Shared prerequisites](Gen3-Self-Hosted-Installation#shared-prerequisites)

---

## 1. Install the Quick Installer

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

## 2. Operator menu

| When you see | Choose |
|--------------|--------|
| **What do you want to do?** | **1** (Install) |
| **Install — choose style** | **1** (Interactive) |

---

## 3. Install wizard

Complete the [shared wizard steps](Gen3-Self-Hosted-Installation#shared-wizard-steps-every-scenario), then use these **ingress-specific** answers:

| When you see | Choose or enter |
|--------------|-----------------|
| **Control Panel — access model** | **2** (NAT & DNS hostname) |
| **Tenant App — access model** | **2** (NAT & DNS hostname) |
| **Control Panel LAN host** (for `:3001` browsing on the LAN) | Node LAN IP (for example `192.168.1.50`) |
| **Control Panel public NAT/DNS hostname** | FQDN only (for example `admin.example.com`) |
| **Tenant App LAN host** (for `:3002` browsing on the LAN) | Node LAN IP (same or different) |
| **Tenant public NAT/DNS hostname** | FQDN only (for example `tenant.example.com`) |

When the tenant is on the open internet, the Control Panel **public** hostname is required so OAuth login redirects work for external users. LAN admins can still use `https://<node-ip>:3001`.

After your last answer, expect **about 15 minutes** before the wizard finishes. Save the bootstrap **email** and **password**.

---

## 4. Log in

**LAN (operators on the internal network):**

- Control Panel: `https://<lan-ip>:3001/login`
- Tenant app: `https://<lan-ip>:3002/login`

**Public internet (emails, external users):**

- Control Panel: `https://<control-panel-fqdn>/login`
- Tenant app: `https://<tenant-fqdn>/login`

Accept self-signed certificate warnings on LAN URLs.

To print bootstrap credentials again:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin bootstrap-creds --namespace <your-namespace>
```

---

## Next step

[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)
