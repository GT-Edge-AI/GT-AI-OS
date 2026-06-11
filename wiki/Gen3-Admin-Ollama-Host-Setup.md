# Ollama Host Setup

## Start Here

1. Pick your **platform preset** below (`4gb-minimum`, `v100-16gb`, `dgx-spark`, or `rtx-pro-6000-96gb`).
2. Run the **one-shot install script** on the Ubuntu GPU host.
3. **Pull models** — always include `embeddinggemma` for GT AI OS embeddings.
4. In Control Panel **Models → Inference Providers**, set the Ollama **base URL** to a cluster-routable address (see [Point GT AI OS at the host](#point-gt-ai-os-at-the-host)).
5. **Discover models** on the Configured Models tab.

## Why this matters

GT AI OS uses Ollama for local embeddings and optional on-prem chat. The Control Panel discovers models from a reachable Ollama root URL (`http://host:11434`, not an OpenAI-style `/v1` path). Pods reach the host through the `local-ollama` bridge when local-network inference is enabled.

## Pick your platform

| Anchor | When to use | Typical VRAM |
| --- | --- | --- |
| [4gb-minimum](#4gb-minimum) | Any Ubuntu host with an NVIDIA GPU **4 GB or larger** | 4–8 GB |
| [v100-16gb](#v100-16gb) | Volta V100 workstation or server | 16 GB |
| [dgx-spark](#dgx-spark) | NVIDIA DGX Spark (GB10, unified memory) | 128 GB UMA |
| [rtx-pro-6000-96gb](#rtx-pro-6000-96gb) | RTX PRO 6000 Blackwell Workstation Edition | 96 GB GDDR7 |

---

## 4gb-minimum

Minimum tier for **Ubuntu + NVIDIA GPU (4 GB+)**. Tuned for a single small chat model plus embeddings.

### Install script

```bash
set -euo pipefail

if ! command -v ollama >/dev/null; then
  curl -fsSL https://ollama.com/install.sh | sh
fi

sudo mkdir -p /etc/systemd/system/ollama.service.d
sudo tee /etc/systemd/system/ollama.service.d/override.conf >/dev/null <<'EOF'
[Service]
# Ubuntu + 4–8 GB GPU (minimum tier)
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=30m"
Environment="OLLAMA_MAX_LOADED_MODELS=1"
Environment="OLLAMA_NUM_PARALLEL=1"
Environment="OLLAMA_CONTEXT_LENGTH=4096"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_GPU_OVERHEAD=536870912"
Environment="OLLAMA_FLASH_ATTENTION=1"
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now ollama
sudo systemctl restart ollama

sudo ufw disable 2>/dev/null || true
sudo systemctl stop ufw 2>/dev/null || true
sudo systemctl disable ufw 2>/dev/null || true
if systemctl list-unit-files firewalld.service &>/dev/null; then
  sudo systemctl stop firewalld
  sudo systemctl disable firewalld
fi

LAN_IP="$(hostname -I | awk '{print $1}')"
echo "==> systemd: $(systemctl is-active ollama)"
curl -fsS http://127.0.0.1:11434/api/tags
curl -fsS "http://${LAN_IP}:11434/api/tags"
ollama ps || true
echo "Done. Next: pull models (see below)."
```

### Pull models

```bash
ollama pull embeddinggemma
ollama pull llama3.2:1b
# or: ollama pull phi3:mini
```

---

## v100-16gb

Volta V100 with **16 GB** VRAM. For **32 GB** cards, set `OLLAMA_MAX_LOADED_MODELS=2` in the override.

### Install script

```bash
set -euo pipefail

if ! command -v ollama >/dev/null; then
  curl -fsSL https://ollama.com/install.sh | sh
fi

sudo mkdir -p /etc/systemd/system/ollama.service.d
sudo tee /etc/systemd/system/ollama.service.d/override.conf >/dev/null <<'EOF'
[Service]
# Volta V100 16 GB
# Multi-GPU: uncomment:
# Environment="CUDA_VISIBLE_DEVICES=0,1,2,3"
# Environment="OLLAMA_SCHED_SPREAD=1"
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=6h"
Environment="OLLAMA_MAX_LOADED_MODELS=1"
Environment="OLLAMA_NUM_PARALLEL=1"
Environment="OLLAMA_CONTEXT_LENGTH=8192"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now ollama
sudo systemctl restart ollama

sudo ufw disable 2>/dev/null || true
sudo systemctl stop ufw 2>/dev/null || true
sudo systemctl disable ufw 2>/dev/null || true
if systemctl list-unit-files firewalld.service &>/dev/null; then
  sudo systemctl stop firewalld
  sudo systemctl disable firewalld
fi

LAN_IP="$(hostname -I | awk '{print $1}')"
echo "==> systemd: $(systemctl is-active ollama)"
curl -fsS http://127.0.0.1:11434/api/tags
curl -fsS "http://${LAN_IP}:11434/api/tags"
ollama ps || true
echo "Done. Next: pull models (see below)."
```

### Pull models

```bash
ollama pull embeddinggemma
ollama pull llama3.2:3b
ollama pull nemotron-mini
```

---

## dgx-spark

NVIDIA DGX Spark (GB10, **128 GB** unified memory). Supports higher concurrency than discrete-GPU tiers.

### Install script

```bash
set -euo pipefail

if ! command -v ollama >/dev/null; then
  curl -fsSL https://ollama.com/install.sh | sh
fi

sudo mkdir -p /etc/systemd/system/ollama.service.d
sudo tee /etc/systemd/system/ollama.service.d/override.conf >/dev/null <<'EOF'
[Service]
# DGX Spark — 128 GB UMA Blackwell
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=6h"
Environment="OLLAMA_MAX_LOADED_MODELS=4"
Environment="OLLAMA_NUM_PARALLEL=4"
Environment="OLLAMA_CONTEXT_LENGTH=16384"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now ollama
sudo systemctl restart ollama

sudo ufw disable 2>/dev/null || true
sudo systemctl stop ufw 2>/dev/null || true
sudo systemctl disable ufw 2>/dev/null || true
if systemctl list-unit-files firewalld.service &>/dev/null; then
  sudo systemctl stop firewalld
  sudo systemctl disable firewalld
fi

LAN_IP="$(hostname -I | awk '{print $1}')"
echo "==> systemd: $(systemctl is-active ollama)"
curl -fsS http://127.0.0.1:11434/api/tags
curl -fsS "http://${LAN_IP}:11434/api/tags"
ollama ps || true
echo "Done. Next: pull models (see below)."
```

### Pull models

```bash
ollama pull embeddinggemma
ollama pull nemotron
ollama pull llama3.3:70b
```

---

## rtx-pro-6000-96gb

NVIDIA **RTX PRO 6000 Blackwell Workstation Edition** (96 GB GDDR7). For **48 GB Max-Q** SKUs, set `OLLAMA_MAX_LOADED_MODELS=2` and `OLLAMA_NUM_PARALLEL=2`.

### Install script

```bash
set -euo pipefail

if ! command -v ollama >/dev/null; then
  curl -fsSL https://ollama.com/install.sh | sh
fi

sudo mkdir -p /etc/systemd/system/ollama.service.d
sudo tee /etc/systemd/system/ollama.service.d/override.conf >/dev/null <<'EOF'
[Service]
# RTX PRO 6000 Blackwell Workstation Edition (96 GB GDDR7)
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=6h"
Environment="OLLAMA_MAX_LOADED_MODELS=3"
Environment="OLLAMA_NUM_PARALLEL=4"
Environment="OLLAMA_CONTEXT_LENGTH=16384"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now ollama
sudo systemctl restart ollama

sudo ufw disable 2>/dev/null || true
sudo systemctl stop ufw 2>/dev/null || true
sudo systemctl disable ufw 2>/dev/null || true
if systemctl list-unit-files firewalld.service &>/dev/null; then
  sudo systemctl stop firewalld
  sudo systemctl disable firewalld
fi

LAN_IP="$(hostname -I | awk '{print $1}')"
echo "==> systemd: $(systemctl is-active ollama)"
curl -fsS http://127.0.0.1:11434/api/tags
curl -fsS "http://${LAN_IP}:11434/api/tags"
ollama ps || true
echo "Done. Next: pull models (see below)."
```

### Pull models

```bash
ollama pull embeddinggemma
ollama pull llama3.3:70b
ollama pull nemotron
```

---

## Model pulls by VRAM (quick reference)

| VRAM tier | Example chat pulls | Embedding (required) |
| --- | --- | --- |
| **4–8 GB** (minimum) | `llama3.2:1b` or `phi3:mini` | `ollama pull embeddinggemma` |
| **16 GB (V100)** | `llama3.2:3b`, `nemotron-mini` | `embeddinggemma` |
| **128 GB UMA (DGX Spark)** | `nemotron`, `llama3.3:70b` | `embeddinggemma` |
| **96 GB (RTX PRO 6000)** | `llama3.3:70b`, `nemotron` | `embeddinggemma` |

Always pull **`embeddinggemma`** before setting the deployment default embedding model in Control Panel.

---

## Point GT AI OS at the host

| Context | Base URL |
| --- | --- |
| **RKE2 / GT AI OS on same host** (local bridge enabled) | `http://local-ollama:11434` |
| **LAN inference host** (pods route to explicit IPv4) | `http://<host-lan-ip>:11434` |
| **On the Ollama host shell** | `http://127.0.0.1:11434` |

In Control Panel **Models → Inference Providers**, edit the Ollama provider:

- **Base URL** must be the server **root** (no `/v1` suffix).
- **Models listing path** is typically `/api/tags` for Ollama.
- Run **Test connection**, then **Discover** on the Configured Models tab.

See also [Models](gen3-admin/models).

---

## Clients on the LAN

| Client | Endpoint style | Notes |
| --- | --- | --- |
| **Ollama native API** | `http://<lan-ip>:11434/api/chat`, `/api/embed`, `/api/tags` | GT AI OS adapter uses native Ollama routes |
| **OpenAI-compatible shim** | `http://<lan-ip>:11434/v1/...` | Optional for external tools; **do not** use `/v1` as the Control Panel base URL |

---

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| **Connection refused** from Control Panel or pods | Confirm `OLLAMA_HOST=0.0.0.0:11434`; host firewall disabled for lab/LAN; `curl http://<lan-ip>:11434/api/tags` from another machine on the LAN |
| **`local-ollama` service missing** | Cluster deployed with local-network inference; `kubectl get svc local-ollama -n <namespace>` |
| **Wrong bridge target IP** | `kubectl get endpointslice -n <namespace> -l kubernetes.io/service-name=local-ollama` — endpoint must match a host IP pods can route to |
| **OOM or 503 under load** | Lower `OLLAMA_NUM_PARALLEL`, then `OLLAMA_MAX_LOADED_MODELS`, then `OLLAMA_CONTEXT_LENGTH` in the systemd override |
| **Empty model list after discovery** | Run `ollama pull embeddinggemma` (and at least one chat model) on the host; retry discovery |
| **DGX / driver issues** | `nvidia-smi` healthy; reinstall NVIDIA driver stack if GPU not visible to Ollama |

After OOM or slow responses: reduce parallelism first, then loaded-model count, then context length.

---

## Security note

Disabling **ufw** / **firewalld** is intended for **trusted lab or LAN** inference hosts. Do not expose port `11434` to the public internet without TLS and access control in front.
