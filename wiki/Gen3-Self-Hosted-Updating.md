# Self-Hosted updating

Upgrade the **application version** in an existing namespace on the install host. This path uses **`gt-ai-os-admin`** only. It does **not** reinstall RKE2.

For installs from **v3.0.2+** public releases (`GT-Edge-AI/GT-AI-OS`, `ghcr.io/gt-edge-ai`), you usually do **not** need a GitHub PAT when release assets and registry images are publicly reachable.

---

## Before you start

- Run commands on the **same host** that installed the cluster (or any host with `/var/lib/gt-ai-os/admin` state and cluster `kubeconfig` access).
- Know your namespace (default **`gt-ai-os-prod`**) and target release tag (for example **`v3.0.3`**).
- List published tags if needed:

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin release list --limit 20
```

Shared operator state lives under **`/var/lib/gt-ai-os/admin`** (auth, `state.json`, generated manifests). Any sudo user on the host can reuse stored credentials after the first successful auth.

---

## Non-interactive upgrade (recommended for automation)

Substitute your namespace and target tag:

```bash
export NAMESPACE="gt-ai-os-prod"
export TO_VERSION="v3.0.3"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin release install-admin-cli --version "${TO_VERSION}"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin update --yes --namespace "${NAMESPACE}" --to "${TO_VERSION}"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin validate --namespace "${NAMESPACE}"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin report --namespace "${NAMESPACE}"
```

`--yes` is required when stdin is not a TTY.

---

## Interactive upgrade

Install the admin CLI for the target tag, then run `update` without `--yes` to confirm namespace and version at prompts:

```bash
export TO_VERSION="v3.0.3"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin release install-admin-cli --version "${TO_VERSION}"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin update --namespace gt-ai-os-prod --to "${TO_VERSION}"
```

Then run **`validate`** and **`report`** as in the non-interactive section.

---

## What `update` does

`gt-ai-os-admin update` loads stored instance state for the namespace, fetches release assets for the `--to` tag, refreshes Helm values and manifests, runs deploy validation and smoke checks (unless disabled), and saves updated state. It upgrades **apps in the existing namespace**; it does not replace the Kubernetes distribution.

Hosted **Cloudflare** modes may prompt for or reuse stored Cloudflare profiles during update. LAN-only installs do not require Cloudflare auth.

---

## Admin CLI only (no app version change)

When release notes say only the **admin CLI** changed:

```bash
export TO_VERSION="v3.0.3"

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin release install-admin-cli --version "${TO_VERSION}"
```

The cluster app version stays the same until you run **`update --to …`**.

---

## Rollback

```bash
sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin rollback --yes --namespace gt-ai-os-prod --to <older-tag>

sudo env GT_AI_OS_ADMIN_CONFIG_DIR=/var/lib/gt-ai-os/admin \
  KUBECONFIG=/etc/rancher/rke2/rke2.yaml \
  PATH="/var/lib/rancher/rke2/bin:/usr/local/bin:$PATH" \
  gt-ai-os-admin validate --namespace gt-ai-os-prod
```

---

## If something fails

| Symptom | Fix |
|---------|-----|
| **401/403** downloading release assets | `gt-ai-os-admin auth register` or `auth github --non-interactive` with a PAT that has **Contents: Read** on `GT-Edge-AI/GT-AI-OS` |
| **`no state stored for namespace`** | Wrong namespace, or missing merged state under `/var/lib/gt-ai-os/admin` — confirm install completed and `state.json` lists your namespace |
| **ImagePullBackOff** after upgrade | Confirm `ghcr.io/gt-edge-ai` images for the target tag are reachable |
| In-app update dashboard | After upgrade, use Control Panel **Instructions** → **Gen 3 Admin — Updates** (product UI, not host CLI) |

---

## Migration from Internal releases (≤ v3.0.1)

Upgrading to **v3.0.2+** rewires release repo and GHCR owner to the public product path. After the first successful **`gt-ai-os-admin update`** to a current tag, re-run **`validate`** and **`report`**.

---

## After upgrade

1. Confirm URLs with **`gt-ai-os-admin report`**.
2. Sign in to Control Panel and tenant app; use **GT AI OS Instructions** and **GT Helper** for day-2 configuration (see [Self-Hosted Control Panel setup](Gen3-Self-Hosted-Control-Panel)).
3. For in-app update dashboards and policies, use Control Panel **Instructions** → **Gen 3 Admin — Updates**.
