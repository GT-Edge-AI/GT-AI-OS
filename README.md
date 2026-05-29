# GT AI OS — customer distribution (3.0.2+)

This repository hosts **customer-facing** GT AI OS release assets, documentation, and install helpers. Application source code remains on `GT-Edge-AI-Internal/gt-ai-os`.

| Path | Purpose |
|------|---------|
| [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) | Helm chart, image bundles, admin CLI, operator script, Quick Installer `.deb`, manifests |
| [Wiki](https://github.com/GT-Edge-AI/GT-AI-OS/wiki) | In-app instructions corpus (Gen 2 + Gen 3 articles) |
| [`agent-templates/`](agent-templates/) | CSV agent templates loaded by the tenant app |

## Quick install (after this repository is public)

**Operator menu (latest release):**

```bash
curl -fsSL https://github.com/GT-Edge-AI/GT-AI-OS/releases/latest/download/gt-ai-os-operator.sh | sudo bash
```

**Quick Installer package (example v3.0.2):**

```bash
curl -fsSL -o /tmp/gt-ai-os.deb \
  https://github.com/GT-Edge-AI/GT-AI-OS/releases/download/v3.0.2/GT-AI-OS-Quick-Installer_3.0.2_all.deb
sudo apt install /tmp/gt-ai-os.deb
gt-ai-os-operator
```

Container images publish to **`ghcr.io/gt-edge-ai/gt-ai-os-*`**. No GitHub PAT is required for install or update once this repository and GHCR packages are public.

## Licensing

Deployment licenses are issued separately (not stored in this repository). Contact your GT Edge AI operator for license delivery and fulfillment runbooks.

## Internal references

- Development repo: `GT-Edge-AI-Internal/gt-ai-os`
- Public release and migration guide: `gt-ai-os/docs/operations/GT3-PUBLIC-RELEASE-AND-INSTALL.md` (in the dev repo)
