# Install — Local Portable

Install GT AI OS on a **Linux laptop** for lab use. **Local Portable** gives you loopback URLs that always work offline, plus LAN URLs on the current WiFi address that **update automatically** when DHCP changes.

[← Back to installation hub](Gen3-Self-Hosted-Installation)

---

## Prerequisites

- **Linux laptop** (Ubuntu or DGX OS 7) with roaming WiFi — **no static LAN IP** required
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`**
- [Shared prerequisites](Gen3-Self-Hosted-Installation#shared-prerequisites)

For a **dedicated server** with a fixed LAN IP, use [Install — Local LAN](Gen3-Self-Hosted-Install-Local-LAN) instead.

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
| **Control Panel — access model** | **4** (Local Portable) |
| **Tenant App — access model** | **4** (Local Portable) |

The wizard autodetects the current LAN IP and enables automatic URL heal when WiFi changes. You do **not** need to enter a static LAN IP.

After your last answer, expect **about 15 minutes** before the wizard finishes. Save the bootstrap **email** and **password**.

---

## 4. Log in

| Situation | URLs |
|-----------|------|
| Solo on the laptop (offline or any network) | `https://127.0.0.1:3001/login` and `https://127.0.0.1:3002/login` |
| On WiFi — LAN peers on the same network | `https://<current-lan-ip>:3001/login` and `:3002` (see `gt-ai-os-admin report` after a DHCP move) |

Accept self-signed certificate warnings.

To print bootstrap credentials again:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin bootstrap-creds --namespace <your-namespace>
```

---

## Next step

[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)
