# GT AI OS

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

GT AI OS is a **self-hosted enterprise AI platform** for **RKE2** (Kubernetes). A **Control Panel** handles administration; a **tenant app** gives users agents, chat, and document/RAG workflows. Data and inference stay in your environment.

This repository has releases and install documentation for **v3.0.2** and later (current stable: **v3.0.7-stable**). Install from [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases); images are on **`ghcr.io/gt-edge-ai`**.

Some capabilities require an **Enterprise license** from [GT Edge AI](https://gtedge.ai/contact-us). See [Enterprise license](#enterprise-license) below.

---

## Installation

Install the **Quick Installer `.deb`**, then run the operator and choose **Install → Interactive**. Commands are the same on Ubuntu and DGX; the wizard asks you to confirm detected host type and architecture.

v3.0.2+ uses **registry-backed** images only. [Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and images on **`ghcr.io/gt-edge-ai`** do **not** require a GitHub PAT.

### Before you install (hosts that already run Gen 2)

LAN / local-dev installs bind **HTTPS** on host ports **`3001`** (Control Panel) and **`3002`** (Tenant App) via `browser-edge`. If **Gen 2** Docker is still running on the same host, its frontends usually publish the same ports over **HTTP** (`gentwo-controlpanel-frontend` → `:3001`, `gentwo-tenant-frontend` → `:3002`). Browsers then fail with TLS errors such as `SSL_ERROR_RX_RECORD_TOO_LONG` / `wrong version number`.

**Stop Gen 2 frontends before installing Gen 3** (or free those ports another way):

```bash
# Confirm Gen 2 is publishing the ports Gen 3 local-dev needs
sudo docker ps --format 'table {{.Names}}\t{{.Ports}}\t{{.Status}}' | grep -E '3001|3002|gentwo' || true

# Free browser ports (minimum required for Gen 3 local-dev)
sudo docker stop gentwo-controlpanel-frontend gentwo-tenant-frontend
sudo docker update --restart=no gentwo-controlpanel-frontend gentwo-tenant-frontend

# Optional: stop all Gen 2 containers on this host
sudo docker ps -q --filter 'name=gentwo-' | xargs -r sudo docker stop
sudo docker ps -aq --filter 'name=gentwo-' | xargs -r sudo docker update --restart=no

# Confirm ports are free
sudo ss -lntp | grep -E ':3001|:3002' || echo "OK: 3001/3002 not listening"
sudo docker ps --format 'table {{.Names}}\t{{.Ports}}' | grep -E '3001|3002' || echo "OK: no docker publishes on 3001/3002"
```
Skip this section if Docker/`gentwo-*` is not present on the install host.

Downloads the [latest published release](https://github.com/GT-Edge-AI/GT-AI-OS/releases/latest). To pin a specific tag, set `TAG` (for example `TAG=v3.0.4`) before running the commands. The `.deb` filename uses semver **without** the `v` prefix (`3.0.4` for tag `v3.0.4`).

```bash
TAG="$(curl -fsSL https://api.github.com/repos/GT-Edge-AI/GT-AI-OS/releases/latest | grep '"tag_name"' | head -1 | cut -d'"' -f4)"
VER="${TAG#v}"
curl -fsSL -o /tmp/gt-ai-os.deb \
  "https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/${TAG}/GT-AI-OS-Quick-Installer_${VER}_all.deb"
sudo apt install -y /tmp/gt-ai-os.deb
sudo -E gt-ai-os-operator
```

**Typical LAN lab prompts:** accept detected host and arch; keep namespace `gt-ai-os-prod`; pick latest release; **LAN only** for Control Panel and Tenant; enter your static LAN IP for both; cluster **auto-detect**; confirm with `y`.

**Full wizard table, validation, and troubleshooting:** [Self-Hosted installation](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Installation)

---

## Update an existing installation

Run these on the **install host** with cluster access. Use the latest published release by default, or set `TO_VERSION` to pin a tag (for example `TO_VERSION=v3.0.4`).

Step 1 refreshes operator scripts from the release, then installs the matching **`gt-ai-os-admin`** for `TO_VERSION` using release assets (safe while the current CLI is still running). Steps 2–3 upgrade the namespace and validate.

```bash
export NAMESPACE="gt-ai-os-prod"
export TO_VERSION="$(curl -fsSL https://api.github.com/repos/GT-Edge-AI/GT-AI-OS/releases/latest | grep '"tag_name"' | head -1 | cut -d'"' -f4)"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  bash -c 'source /var/lib/gt-ai-os/operator-scripts/gt-ai-os-admin-env.sh && gt_ai_os_ensure_admin_cli_version "'"${TO_VERSION}"'"'

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin update --yes --namespace "${NAMESPACE}" --to "${TO_VERSION}"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin validate --namespace "${NAMESPACE}"
```

**Interactive upgrade** (menu prompts for namespace and release): `sudo bash /var/lib/gt-ai-os/operator-scripts/manage-ai-os.sh upgrade`

**v3.0.4 — known CLI messages (cosmetic):** `the database system is shutting down` during `update` is normal while CNPG restarts—wait a few minutes and let it finish. `tenant DB migration version is 45, expected 44` on `validate` is a false alarm if the host still has an older `gt-ai-os-admin` (run step 1). Neither blocks the upgrade; the namespace still reaches **v3.0.4** and the apps come up.

**Rollback and troubleshooting:** [Self-Hosted updating](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Updating)

---

## Access

Local-network installs (typical lab / LAN HTTPS):

| App | URL | Default login (first install) |
|-----|-----|-------------------------------|
| Control Panel | `https://<host>:3001/login` | `gtadmin@test.com` / `Test@123` |
| Tenant App | `https://<host>:3002/login` | `gtadmin@test.com` / `Test@123` |

Replace `<host>` with the **fixed LAN IP** you set at install time. Accept the self-signed certificate warning in the browser.

### Next steps

1. Complete first-time setup: [Self-Hosted Control Panel setup](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Control-Panel)
2. In Control Panel, open **Instructions** (sidebar) and **? GT Helper** — start with **Gen 3 Admin Getting Started** ([wiki mirror](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Admin-Getting-Started))
3. In the tenant app, open **GT AI OS Instructions** → **Gen 3 Getting Started** ([wiki mirror](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Started)) for agents, chat, and datasets
4. Change default passwords before production use

---

## Platform requirements

| Platform | Architecture | Minimum resources |
|----------|--------------|-------------------|
| **Ubuntu** 24.04 | x86_64 | 8+ CPU cores, 16 GB RAM, 100 GB disk |
| **DGX OS 7** | ARM64 (Grace) | Same command flow; confirm arch when prompted |
| **Production HA** | Multi-node RKE2 | Per release manifest |

Clusters must reach **`ghcr.io/gt-edge-ai`** (or your approved mirror). Databases require a StorageClass suitable for CloudNativePG (for example Longhorn with immediate volume binding). See the [installation runbook](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Installation) for prerequisites and troubleshooting.

---

## Runtime images

| Topic | Detail |
|-------|--------|
| **Registry** | `ghcr.io/gt-edge-ai/gt-ai-os-*` tagged to match the release (for example `v3.0.4`) |
| **Helm / manifest** | `gt-ai-os-v<version>.tgz` and `release-manifest.json` on each [Release](https://github.com/GT-Edge-AI/GT-AI-OS/releases) |
| **Image bundles** | Not published for v3.0.2+ |

---

## Features

- **Agent builder** — Custom agents, templates, role-based access, and guardrails
- **Datasets and RAG** — Document-centric chat with retrieval-augmented generation
- **GT API** — OpenAI-compatible API for integrated applications (documented in **GT AI OS Instructions** when GT API is enabled)
- **Teams and sharing** — Workgroup access to agents and datasets
- **Observability** — Usage dashboards, conversation review, and operational metrics
- **Enterprise controls** — SSO, compliance mode, billing, and GT API (license required; see below)

---

## Enterprise license

You can install and use GT AI OS **without a license** for evaluation, with **low user limits**. An **Enterprise license** raises seat limits and unlocks the integrations below. Licenses are **not** included in this repository—you request one from GT Edge AI and activate it on the Control Panel **License** page.

**Contact GT Edge AI** to request a license for your deployment: [gtedge.ai/contact-us](https://gtedge.ai/contact-us).

| Area | Requires Enterprise license |
|------|----------------------------|
| **Control Panel — SSO** | Identity providers and SCIM provisioning |
| **Control Panel — Compliance mode** | Compliance configuration |
| **Control Panel — Financial controls** | Billing policy, allocations, and related broadcasts |
| **Tenant app — GT API** | API keys and external application integrations (also enable GT API for the tenant) |
| **Tenant app — Billing** | Usage billing views and allocations (tenant owner) |

**Included without a license** (subject to seat caps): install and updates, agents, chat, RAG, datasets, models, teams, backup/restore, and most observability (billing tabs stay hidden until licensed).

After you receive a license file, open **Control Panel → License**, upload it, and confirm the status shows active before using the features above.

---

## Documentation

| Phase | Where to read |
|-------|----------------|
| **Install, update, Control Panel setup (host)** | [Self-Hosted installation](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Installation) · [Self-Hosted updating](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Updating) · [Self-Hosted Control Panel setup](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Self-Hosted-Control-Panel) |
| **Operate Control Panel (in-app)** | After login: **Instructions** + **? GT Helper** — [Gen 3 Admin Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Admin-Getting-Started) |
| **Use the tenant app (in-app)** | **GT AI OS Instructions** — [Gen 3 Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Started), [Chat](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Chat), [Agents](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Agents) |
| **Issues** | [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues); operator troubleshooting via **Instructions** / GT Helper ([Super Admin Troubleshooting](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Super-Admin-Troubleshooting) when published) |

In-app **GT AI OS Instructions** and **GT Helper** use the same Gen 3 wiki corpus; open them from the Control Panel or tenant UI after setup rather than relying on host runbooks for day-to-day product tasks.

---

## Quick commands

```bash
sudo -E gt-ai-os-operator                                    # Install menu (after .deb install)
sudo bash /var/lib/gt-ai-os/operator-scripts/manage-ai-os.sh upgrade  # Interactive namespace upgrade
gt-ai-os-admin release list --limit 20                       # Published release tags
gt-ai-os-admin report --namespace <ns>                       # URLs and status
gt-ai-os-admin validate --namespace <ns>                     # Post-install or post-update checks
sudo gt-ai-os-operator --nuke --yes                          # Remove install (lab reset)
```

---

## Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                          GT AI OS                              │
├──────────────────┬──────────────────────┬──────────────────────┤
│   Control Panel  │      Tenant App      │   Resource Cluster   │
│    (Admin UI)    │       (User UI)      │ (AI inference routing)│
├──────────────────┴──────────────────────┴──────────────────────┤
│                         PostgreSQL                              │
│                  Control DB  │  Tenant DB                       │
└────────────────────────────────────────────────────────────────┘
```

---

## Support

- **Runbook issues:** [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues)
- **In-app:** Tenant **Instructions** and **Contact support** (when configured by your operator)
- **Security:** [SECURITY.md](SECURITY.md) and [contact GT Edge AI](https://gtedge.ai/contact-us)
- **Licensing:** [Request an Enterprise license](https://gtedge.ai/contact-us) from GT Edge AI; activate on Control Panel → **License**

---

## License

Apache License 2.0 — see [LICENSE](LICENSE).

---

**GT AI OS** · [GT Edge AI](https://gtedge.ai)
