# GT AI OS

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

GT AI OS is a **self-hosted enterprise AI platform** for **RKE2** (Kubernetes). A **Control Panel** handles administration; a **tenant app** gives users agents, chat, and document/RAG workflows. Data and inference stay in your environment.

This repository has releases and install documentation for **v3.0.2** and later. Install from [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases); images are on **`ghcr.io/gt-edge-ai`**.

Some capabilities require an **Enterprise license** from [GT Edge AI](https://gtedge.ai/contact-us). See [Enterprise license](#enterprise-license) below.

---

## Installation

Choose your platform for detailed runbooks in the wiki, then use one install entry point below.

| Platform | Guide |
|----------|-------|
| **Ubuntu** 24.04 (x86_64) | [Installation — Ubuntu](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation#ubuntu-installation) |
| **NVIDIA DGX OS 7** (ARM64) | [Installation — DGX](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation#dgx-installation) |

| Method | Use when |
|--------|----------|
| **Operator script** | Interactive or scripted install on a fresh RKE2 host |
| **Quick Installer `.deb`** | You want `gt-ai-os-operator` installed via apt |
| **`gt-ai-os-admin` CLI** | Fully non-interactive install from release tarballs |

**Start here:** [Installation (wiki)](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation) · [Gen 3 Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Started)

v3.0.2+ uses **registry-backed** images only (no per-platform image bundle tarballs). While this repository is private, use `gh auth` or a release-read token; after the repository and GHCR are public, token-free install is supported.

**Operator (public repo):**

```bash
curl -fsSL https://github.com/GT-Edge-AI/GT-AI-OS/releases/latest/download/gt-ai-os-operator.sh | sudo bash
```

## Update an existing installation

**Ubuntu / DGX (operator menu):**

```bash
sudo gt-ai-os-admin update --yes --namespace <namespace-name> --to latest
```

**Validate after upgrade:**

```bash
sudo gt-ai-os-operator --validate --namespace <namespace> --lan-ip <your-lan-ip>
```

For troubleshooting, see [Updating](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Updating) and [Gen 3 Admin — Updates](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Admin-Updates).

---

## Access

Local-network installs (typical lab / LAN HTTPS):

| App | URL | Default login (first install) |
|-----|-----|-------------------------------|
| Control Panel | `https://<host>:3001/login` | `gtadmin@test.com` / `Test@123` |
| Tenant App | `https://<host>:3002/login` | `gtadmin@test.com` / `Test@123` |

Replace `<host>` with the **fixed LAN IP** you set at install time. Change default passwords before production use. Accept the self-signed certificate warning in the browser.

---

## Platform requirements

| Platform | Architecture | Minimum resources |
|----------|--------------|-------------------|
| **Ubuntu** 24.04 | x86_64 | 8+ CPU cores, 16 GB RAM, 100 GB disk (see wiki) |
| **DGX OS 7** | ARM64 (Grace) | See [DGX installation guide](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation#dgx-installation) |
| **Production HA** | Multi-node RKE2 | Per release manifest and wiki |

Clusters must reach **`ghcr.io/gt-edge-ai`** (or your approved mirror). Databases require a StorageClass suitable for CloudNativePG (for example Longhorn with immediate volume binding). Details are in the wiki.

---

## Runtime images

| Topic | Detail |
|-------|--------|
| **Registry** | `ghcr.io/gt-edge-ai/gt-ai-os-*` tagged to match the release (for example `v3.0.2`) |
| **Helm / manifest** | `gt-ai-os-v<version>.tgz` and `release-manifest.json` on each [Release](https://github.com/GT-Edge-AI/GT-AI-OS/releases) |
| **Image bundles** | Not published for v3.0.2+ |

---

## Features

- **Agent builder** — Custom agents, templates, role-based access, and guardrails
- **Datasets and RAG** — Document-centric chat with retrieval-augmented generation
- **GT API** — OpenAI-compatible API for integrated applications (see wiki)
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

Full guides are in the **[wiki](https://github.com/GT-Edge-AI/GT-AI-OS/wiki)**:

| Topic | Description |
|-------|-------------|
| [Gen 3 Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Started) | Primary guide for RKE2 deployments |
| [Gen 3 Admin Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Admin-Getting-Started) | Control Panel administration |
| [Gen 3 Chat](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Chat) | Tenant chat and conversations |
| [Gen 3 Agents](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Agents) | Agent configuration and templates |
| [Gen 3 GT API Overview](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Gt-Api-Overview) | API keys and compatibility |
| [Installation](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation) | Platform install runbooks |
| [Updating](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Updating) | Upgrade an existing deployment |
| [Troubleshooting](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Super-Admin-Troubleshooting) | Common issues |

Legacy Gen 2 wiki articles remain for reference during migration; prefer Gen 3 articles for new installs.

---

## Quick commands

```bash
gt-ai-os-operator                    # Install / update menu (use sudo -E when needed)
gt-ai-os-admin report --namespace <ns>   # URLs and status
gt-ai-os-admin validate --namespace <ns> # Post-install checks
sudo gt-ai-os-operator --nuke --yes  # Remove install (lab reset)
```

---

## Migration from Internal releases (≤ v3.0.1)

| Version | Release host | GHCR owner |
|---------|--------------|------------|
| ≤ v3.0.1 | `GT-Edge-AI-Internal/gt-ai-os-release` | `gt-edge-ai-internal` |
| ≥ v3.0.2 | **This repository** | `gt-edge-ai` |

v3.0.2 does not dual-publish to the Internal release repository. Use the supported upgrade path to rewire release repo, GHCR owner, and registry pulls.

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
