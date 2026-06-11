# Self-Hosted installation

Choose one install runbook below. Each runbook takes you from a fresh Ubuntu or DGX host through the interactive operator wizard to your first **Control Panel** login.

After install, complete the Control Panel **QuickStart** wizard (`/dashboard/quickstart`) — see [Control Panel QuickStart](Gen3-Admin-Quickstart). Optionally apply the universal free-tier baseline before first login:

```bash
gt-ai-os-admin install --baseline   # apply defaults at end of guided install
# or after any successful install:
gt-ai-os-admin setup-baseline-apply --namespace <namespace> --yes
```

The interactive `install-ai-os.sh` script prompts for baseline apply when run on a TTY. Continue to [Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel). To upgrade an existing host, see [Self-Hosted updating](Gen3-Self-Hosted-Updating).

---

## Install runbooks

| Scenario | Runbook | When to use |
|----------|---------|-------------|
| **Local LAN** | [Install — Local LAN](Gen3-Self-Hosted-Install-Local-LAN) | Operators reach Control Panel and the tenant app on the node LAN IP (`https://<ip>:3001` and `:3002`). |
| **Cloudflare** | [Install — Cloudflare](Gen3-Self-Hosted-Install-Cloudflare) | Internet users reach both apps through Cloudflare Tunnel on public hostnames. |

---

## Shared prerequisites

Every scenario needs:

- **Ubuntu 24.04** (x86_64) or **DGX OS 7** (ARM64): 8+ CPU cores, 16 GB RAM, 100 GB disk recommended
- Outbound HTTPS to [GitHub Releases](https://github.com/GT-Edge-AI/GT-AI-OS/releases) and **`ghcr.io/gt-edge-ai`**

Each scenario runbook lists any extra prerequisites (LAN IP or Cloudflare).

---

## Troubleshooting

| Symptom | What to check |
|---------|----------------|
| **ImagePullBackOff** | Cluster must pull `ghcr.io/gt-edge-ai/gt-ai-os-*:<tag>`; GHCR packages must be public |
| Release download **401/403** | Outbound HTTPS to `github.com`; proxy or firewall blocking anonymous release access |
| Database pods pending | StorageClass and volume binding for CloudNativePG |
| Wrong URLs after install | `gt-ai-os-admin report --namespace <your-namespace>` |

Report runbook gaps on [GitHub Issues](https://github.com/GT-Edge-AI/GT-AI-OS/issues).
