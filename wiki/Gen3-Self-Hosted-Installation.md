# Self-Hosted installation

Choose one install runbook below. Each runbook takes you from a fresh Ubuntu or DGX host through the interactive operator wizard to your first **Control Panel** login.

After install, continue to [Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel). To upgrade an existing host, see [Self-Hosted updating](Gen3-Self-Hosted-Updating).

---

## How ingress works in the installer

The interactive wizard asks for **Control Panel** and **Tenant App** access **separately**. For each app, pick one of four models:

| # | Access model | When to use |
|---|--------------|-------------|
| **1** | **LAN only** | Browsers on the same network open `https://<node-ip>:3001` (Control Panel) or `:3002` (Tenant). The wizard autodetects the node IP when possible. |
| **2** | **NAT & DNS hostname** | Open-internet users browse portless `https://<fqdn>` on public **443** (firewall NAT → `:3001` / `:3002`). LAN operators can still use `https://<node-ip>:3001` and `:3002`. |
| **3** | **Cloudflare tunnel** | Public internet access via **Cloudflare Tunnel** and DNS hostnames (not raw port forwarding). |
| **4** | **Local Portable** | Linux **laptop** lab installs: `https://127.0.0.1:3001` / `:3002` always work; LAN URLs follow roaming WiFi (DHCP) automatically. |

If **any** app uses Cloudflare, the wizard asks for **one** Cloudflare profile (**commercial** or **government**) that applies to every Cloudflare app in that install. Do not mix commercial and government accounts or tokens in one install.

You can mix models per app (for example Control Panel on LAN and Tenant on Cloudflare). See [Install — mixed ingress](Gen3-Self-Hosted-Install-Mixed).

---

## Install runbooks

| Scenario | Runbook | Wizard choices (summary) |
|----------|---------|--------------------------|
| **LAN lab / server** | [Install — Local LAN](Gen3-Self-Hosted-Install-Local-LAN) | Both apps: **1) LAN only** |
| **Roaming laptop** | [Install — Local Portable](Gen3-Self-Hosted-Install-Local-Portable) | Both apps: **4) Local Portable** |
| **Public FQDN + NAT** | [Install — NAT & DNS](Gen3-Self-Hosted-Install-NAT-DNS) | Both apps: **2) NAT & DNS hostname** |
| **Cloudflare Tunnel** | [Install — Cloudflare](Gen3-Self-Hosted-Install-Cloudflare) | Both apps: **3) Cloudflare tunnel** |
| **Mixed per-app** | [Install — mixed ingress](Gen3-Self-Hosted-Install-Mixed) | Different models per app (common: CP **LAN**, Tenant **Cloudflare** or **NAT & DNS**) |

---

## Shared wizard steps (every scenario)

After you install the Quick Installer and choose **Install → Interactive**, every runbook shares these prompts:

| When you see | Choose or enter |
|--------------|-----------------|
| **Detected host** — use this? | **Y** (or pick Ubuntu, DGX OS 7, or Ubuntu on WSL2 if autodetect is wrong) |
| **Detected architecture** — use this package? | **Y** (`linux-amd64` or `linux-arm64`) |
| **Kubernetes namespace** | Your namespace (for example `gt-ai-os-prod`) or **Enter** for the default |
| **Choose a release** | Your release tag (for example **v3.0.4**) |
| **Control Panel — access model** | See your runbook (**1–4**) |
| **Tenant App — access model** | See your runbook (**1–4**) |
| **How should GT AI OS use Kubernetes?** | **1** (Auto-detect) on a clean host |
| **Fresh install vs Resume** (if RKE2 is already running) | **1** Fresh; **2** Resume |
| **Wipe vs Abort** (if RKE2 artifacts exist but the API is down) | **1** Wipe |
| **Ready to install?** | **y** |

Scenario-specific hostname, NAT, or Cloudflare prompts come **after** the per-app access model choices. Expect **about 15 minutes** after your last answer before the wizard finishes.

---

## Shared prerequisites

Every scenario needs:

- **Ubuntu 24.04** (x86_64) or **DGX OS 7** (x86_64 or ARM64): 8+ CPU cores, 16 GB RAM, 100 GB disk recommended
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`**

Additional prerequisites by scenario:

| Scenario | Also required |
|----------|----------------|
| **Local LAN** | Static **LAN IP** on a dedicated server (recommended); accept browser self-signed cert warnings |
| **Local Portable** | Linux laptop with roaming WiFi; no static IP required |
| **NAT & DNS** | Public DNS A records, firewall **443 → :3001 / :3002** on the node |
| **Cloudflare** | Cloudflare account, API token, account ID, and two public hostnames |
| **Mixed** | Combination of the above for each app’s model |

---

## Troubleshooting

| Symptom | What to check |
|---------|----------------|
| **ImagePullBackOff** | Cluster must pull `ghcr.io/gt-edge-ai/gt-ai-os-*:<tag>`; GHCR packages must be public |
| Release download **401/403** | Outbound HTTPS to `github.com`; proxy or firewall blocking anonymous release access |
| Database pods pending | StorageClass and volume binding for CloudNativePG |
| Wrong URLs after install | `gt-ai-os-admin report --namespace <your-namespace>` |
| Public DNS hostname rejected on LAN-only | Use **NAT & DNS hostname** (option **2**), not **LAN only** (option **1**) |
| Mixed ingress / OAuth redirect errors | When Tenant is public and Control Panel stays on LAN, ensure Control Panel public hostname is set for NAT+DNS tenant installs |

Report runbook gaps on [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues).
