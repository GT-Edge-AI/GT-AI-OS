# Install — Local LAN

Install GT AI OS on a single host so operators open Control Panel and the tenant app on the node **LAN IP** over HTTPS ports **3001** and **3002**.

[← Back to installation hub](Gen3-Self-Hosted-Installation)

---

## Prerequisites

- Static **LAN IP** for the node
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`**
- [Shared prerequisites](Gen3-Self-Hosted-Installation#shared-prerequisites) (Ubuntu or DGX, storage, and so on)

---

## 1. Install the Quick Installer

To pin a release, set `TAG` before download (for example `TAG=v3.0.3`). The `.deb` filename uses semver **without** the `v` prefix (`3.0.3` for tag `v3.0.3`).

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

When the operator menu appears, choose the following:

| When you see | Choose |
|--------------|--------|
| **What do you want to do?** | **1** (Install) |
| **Install — choose style** | **1** (Interactive) |

---

## 3. Install wizard

When the install wizard prompts you, choose or enter the following:

| When you see | Choose or enter |
|--------------|-----------------|
| **Detected host** — use this? | **Y** |
| **Detected architecture** — use this package? | **Y** |
| **Kubernetes namespace** | Your namespace (for example `gt-ai-os-prod`) or **Enter** for the default |
| **Choose a release** | Your release tag (for example **v3.0.3**) |
| **Deployment edge / access mode** | **1** |
| **Expose host over HTTPS to LAN?** | **y** |
| **Control Panel LAN host** (no `https://`, no `:3001`) | Node LAN IP (for example `192.168.1.50`) |
| **Tenant App LAN host** | Same IP (**Enter**) or a different LAN host if needed |
| **How should GT AI OS use Kubernetes?** | **1** (Auto-detect) on a clean host |
| **Fresh install vs Resume** (if RKE2 is already running) | **1** Fresh; **2** Resume |
| **Wipe vs Abort** (if RKE2 artifacts exist but the API is down) | **1** Wipe |
| **Ready to install?** | **y** |

After your last answer above, the install runs automatically. Expect **about 15 minutes** before the wizard finishes. Do not interrupt the terminal.

Save the **bootstrap Control Panel email** and **password** printed when the install finishes.

---

## 4. Log in to Control Panel

1. Open `https://<lan-ip>:3001/login` in your browser (use the LAN IP from the wizard).
2. Sign in with the bootstrap **email** and **password** from step 3.

Accept the browser **self-signed certificate** warning.

To print bootstrap credentials again:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin bootstrap-creds --namespace <your-namespace>
```

Tenant app URL: `https://<lan-ip>:3002/login`

---

## Next step

[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)
