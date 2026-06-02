# Self-Hosted installation

Host-level install for GT AI OS on a single machine using the **Quick Installer `.deb`** and the **interactive** operator wizard. Commands are the same on Ubuntu and NVIDIA DGX; the wizard only asks you to confirm detected host type and CPU architecture.

For post-install Control Panel setup and handoff to **GT AI OS Instructions** and **GT Helper**, continue to [Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel).

---

## Prerequisites

- **Ubuntu 24.04** (x86_64) or **DGX OS 7** (ARM64): 8+ CPU cores, 16 GB RAM, 100 GB disk recommended
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`** (or your approved mirror)
- A **static LAN IP** you will use for HTTPS access on ports **3001** (Control Panel) and **3002** (tenant app)
- StorageClass suitable for CloudNativePG (for example Longhorn with immediate volume binding)

v3.0.2+ uses **registry-backed** images only. Public releases on `GT-Edge-AI/GT-AI-OS` do **not** require a GitHub PAT when release assets and GHCR packages are publicly reachable.

---

## Quick Installer (.deb)

Replace `v3.0.3` with your target [release tag](https://github.com/GT-Edge-AI/GT-AI-OS/releases). The `.deb` filename uses semver **without** the `v` prefix (for example `3.0.3` for tag `v3.0.3`).

```bash
curl -fsSL -o /tmp/gt-ai-os.deb \
  https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/v3.0.3/GT-AI-OS-Quick-Installer_3.0.3_all.deb
sudo apt install -y /tmp/gt-ai-os.deb
sudo -E gt-ai-os-operator
```

At the operator menu choose **1) Install**, then **1) Interactive** (recommended).

---

## Operator menu (before the install wizard)

| Prompt | Recommended answer |
|--------|-------------------|
| What do you want to do? | **1** Install |
| Install — choose style | **1** Interactive |
| GitHub personal access token | **Skip** if anonymous download from `GT-Edge-AI/GT-AI-OS` works; otherwise paste a fine-grained PAT with **Contents: Read** on that repo |

---

## Interactive install wizard (`install-ai-os.sh`)

### Host and release

| Prompt | Default | Recommended |
|--------|---------|-------------|
| Detected host type — use this? | Y | **Y** (Ubuntu or DGX as detected) |
| Select host type (if not detected) | [1] | **1** Ubuntu or **2** DGX OS 7 |
| Detected architecture — use this package? | Y | **Y** (`linux-amd64` or `linux-arm64`) |
| Kubernetes namespace | `gt-ai-os-prod` | **Enter** to keep default |
| GitHub authentication (if prompted) | [1] PAT / [2] `gh` login | Usually **skipped** on public releases; if shown, **1** or **2** |
| Choose a release | [1] = latest | **1** or Enter |

### Per-app access (typical LAN lab)

| Prompt | Default | Recommended |
|--------|---------|-------------|
| Control Panel — access model | [1] | **1** LAN only |
| Tenant App — access model | [1] | **1** LAN only |
| Control Panel LAN host | auto-detected IP | Your **static LAN IP** (no `https://`, no `:3001`) |
| Tenant App LAN host | same as Control Panel | **Enter** (same IP) |

**NAT & DNS** or **Cloudflare** choices add FQDN, profile, and API token prompts. Use those only when you need public hostnames or tunnels; the wizard walks through each field after you select **2** or **3**.

### Kubernetes target

| Prompt | When shown | Recommended |
|--------|------------|-------------|
| How should GT AI OS use Kubernetes? | Always (unless env preset) | **1** Auto-detect |
| Fresh install vs Resume | RKE2 already running, one node | **1** Fresh on clean host; **2** Resume to keep cluster |
| Wipe and install fresh vs Abort | RKE2 artifacts but API down | **1** Wipe for broken reinstall |
| Proceed with namespace-only install? | Existing multi-node cluster | **Y** only if you intend namespace-only |

On a **clean host**, auto-detect bootstraps a **single-node RKE2** cluster without extra prompts.

### Confirm

| Prompt | Recommended |
|--------|-------------|
| Ready to install? `(y/N)` | **y** |

Install then runs packages, Helm, and validation. **`gt-ai-os-admin`** is installed to `/usr/local/bin` as part of this flow.

### Optional environment presets

To skip LAN host prompts:

```bash
export GT_AI_OS_CONTROL_PANEL_LOCAL_EDGE_HOST="<your-lan-ip>"
export GT_AI_OS_TENANT_APP_LOCAL_EDGE_HOST="<your-lan-ip>"
```

---

## After the wizard finishes

### URLs and default login

| App | URL | First login |
|-----|-----|-------------|
| Control Panel | `https://<lan-ip>:3001/login` | `gtadmin@test.com` / `Test@123` |
| Tenant app | `https://<lan-ip>:3002/login` | `gtadmin@test.com` / `Test@123` |

Accept the browser **self-signed certificate** warning for local HTTPS.

### Validate from the host

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin validate --namespace gt-ai-os-prod

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin report --namespace gt-ai-os-prod
```

Replace `gt-ai-os-prod` if you chose another namespace.

---

## Troubleshooting

| Symptom | What to check |
|---------|----------------|
| **ImagePullBackOff** on app pods | Cluster must pull `ghcr.io/gt-edge-ai/gt-ai-os-*:<tag>`; packages must be **public** or `ghcr-pull` configured |
| Release download **401/403** | Register GitHub auth once: `gt-ai-os-admin auth register` (or paste PAT when the wizard prompts) |
| Database pods pending | StorageClass and volume binding for CloudNativePG |
| Wrong URLs after install | Re-run `gt-ai-os-admin report --namespace <ns>`; confirm LAN IP matches install prompts |

Report install runbook gaps on [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues).

---

## Next step

Continue to **[Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)** for passwords, license, models, and enabling **GT Helper** before inviting tenant users.
