# GT AI OS

Enterprise AI platform for **RKE2** — single-tenant deployments with Control Panel administration, tenant workspaces, and optional GT API integrations.

This repository is the **public distribution** for GT AI OS **v3.0.2 and later**: versioned install assets, in-app instructions, and agent templates. Application source code is not published here; operators install from [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and pull container images from GitHub Container Registry.

---

## Installation

Choose one entry point. All paths use the same release tag and **registry-backed** runtime images (`ghcr.io/gt-edge-ai`). No GitHub personal access token is required once this repository and GHCR packages are public.

| Method | Best for |
|--------|----------|
| **Operator script** (menu or flags) | Fast bootstrap on Ubuntu or DGX; single- or multi-node RKE2 |
| **Quick Installer `.deb`** | Apt-based hosts that want `gt-ai-os-operator` on `PATH` |
| **`gt-ai-os-admin` CLI** | Scripted install, update, validate, and rollback from release tarballs |

### Operator script (latest release)

```bash
curl -fsSL https://github.com/GT-Edge-AI/GT-AI-OS/releases/latest/download/gt-ai-os-operator.sh | sudo bash
```

Non-interactive example (adjust namespace, version, and network settings per your runbook):

```bash
sudo bash gt-ai-os-operator.sh --version v3.0.2 --namespace gt-ai-os-prod
```

### Quick Installer (tagged example: v3.0.2)

```bash
curl -fsSL -o /tmp/gt-ai-os.deb \
  https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/v3.0.2/GT-AI-OS-Quick-Installer_3.0.2_all.deb
sudo apt install /tmp/gt-ai-os.deb
gt-ai-os-operator
```

### Admin CLI (from a release asset)

Download `gt-ai-os-admin-linux-amd64-v3.0.2.tar.gz` or `gt-ai-os-admin-linux-arm64-v3.0.2.tar.gz` from [Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases), verify `SHA256SUMS`, extract, and follow your platform install guide in the wiki.

---

## Container images

Runtime workloads pull from **`ghcr.io/gt-edge-ai`** (for example `ghcr.io/gt-edge-ai/gt-ai-os-control-panel:v3.0.2`). The Helm chart and `release-manifest.json` on each release pin compatible image names and tags. **Image bundle tarballs are not published** for v3.0.2+; clusters must reach GHCR (or use your air-gap mirror of those images).

---

## What's in this repository

| Location | Purpose |
|----------|---------|
| [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) | Helm chart (`gt-ai-os-*.tgz`), `gt-ai-os-admin`, operator script, operator-scripts tarball, Quick Installer `.deb`, `release-manifest.json`, checksums |
| [Wiki](https://github.com/GT-Edge-AI/GT-AI-OS/wiki) | In-app instructions (Gen 2 and Gen 3 articles) |
| [`agent-templates/`](agent-templates/) | CSV agent templates loaded by the tenant app |

---

## Documentation

Primary operator and user documentation lives in the **[Wiki](https://github.com/GT-Edge-AI/GT-AI-OS/wiki)**. Start here:

**Gen 3 — getting started**

| Topic | Article |
|-------|---------|
| Overview | [Gen 3 Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Started) |
| Control Panel admin | [Gen 3 Admin Getting Started](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Admin-Getting-Started) |
| Chat and agents | [Gen 3 Chat](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Chat), [Gen 3 Agents](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Agents) |
| GT API | [Gen 3 GT API Overview](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Gt-Api-Overview) |
| Support | [Gen 3 Getting Support](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Gen3-Getting-Support) |

**Gen 2 — legacy articles**

Older Docker Compose–era articles remain for reference during migration. Prefer Gen 3 articles for RKE2 deployments.

| Topic | Article |
|-------|---------|
| Installation (legacy) | [Installation](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Installation) |
| Updating (legacy) | [Updating](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Updating) |
| Troubleshooting | [Super Admin Troubleshooting](https://github.com/GT-Edge-AI/GT-AI-OS/wiki/Super-Admin-Troubleshooting) |

---

## Updating an existing installation

After the initial install, use the operator menu or admin CLI from a **newer release tag** on this repository. Upgrading from **v3.0.1** (Internal release host) to **v3.0.2+** rewires release repo, GHCR owner, and registry pull defaults automatically when you run the supported upgrade path.

```bash
sudo gt-ai-os-operator --update-interactive --version latest
```

Confirm the target version in your change window; validate the cluster before promoting production traffic.

---

## Platform requirements

GT AI OS 3.0 targets **RKE2** on Linux. Typical footprints:

| Platform | Architecture | Notes |
|----------|--------------|--------|
| Ubuntu server | x86_64 | Common single-node and multi-node installs |
| NVIDIA DGX OS | x86_64 or ARM64 | Use arm64 admin CLI and images where applicable |
| Production HA | Multi-node RKE2 | See wiki and release manifest for supported topologies |

Storage for databases should use a StorageClass suitable for CloudNativePG (for example Longhorn with immediate binding). Details are in the wiki and release validation checklist.

---

## Licensing

**Deployment licenses** are issued separately and are not stored in this repository. Contact your GT Edge AI operator for license delivery.

Documentation and template content in this repository are provided for use with licensed GT AI OS deployments. See [LICENSE](LICENSE) if present in this repository root.

---

## Support

- **In-app:** Tenant **Instructions** and **Contact support** (when configured by your operator).
- **Issues:** [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues) on this repository for public distribution feedback.
- **Organization:** Your Tenant Admin or platform operator for deployment-specific incidents.

---

## Upgrading from Internal distribution (v3.0.1 and earlier)

| Version | Release host | GHCR owner |
|---------|--------------|------------|
| ≤ v3.0.1 | `GT-Edge-AI-Internal/gt-ai-os-release` | `gt-edge-ai-internal` |
| ≥ v3.0.2 | **This repository** | `ghcr.io/gt-edge-ai` |

v3.0.2 does not dual-publish to the Internal release repository. Plan a single maintenance window to move to this repo and public GHCR pulls.
