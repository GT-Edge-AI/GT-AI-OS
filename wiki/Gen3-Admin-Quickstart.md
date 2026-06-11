# Control Panel QuickStart

## Purpose

The **QuickStart** setup guide walks Super Admins through first-time Control Panel configuration after install. A **sequential overlay coach** (Setup guide panel) stays on screen while you work on each real page — Models, Users, Email Settings, and so on. It prioritizes **free-tier** inference from **Groq Cloud** and **NVIDIA NIM**, optional local **Ollama**, platform **default models**, users, SMTP, and GT Helper settings.

## When to use QuickStart

1. Immediately after your first Super Admin login — the coach opens automatically. You may **Pause setup** and resume from the sidebar **QuickStart** item or **Continue setup** on `/dashboard/quickstart`.
2. Whenever default models, API keys, or inference providers are incomplete.

## How the coach works

- **One step at a time** — plain-language instructions (“do this, then that”).
- **Next** takes you to the right Control Panel page for the current step.
- **Automatic progress** — when a step is detected complete (for example a Groq API key saved), the coach advances.
- **Overview** — `/dashboard/quickstart` lists all steps and percent complete.

## Step overview

| Step | What you configure |
| --- | --- |
| Welcome | Overview and exit warning |
| Apply baseline | Universal free-tier bundle (models + pricing sheet + default IDs) |
| Deployment profile | Hosted, self-hosted/LAN, or DGX — adjusts Ollama/NIM emphasis |
| Groq API key | Free-tier `gsk_` key from [console.groq.com](https://console.groq.com) |
| NVIDIA NIM API key | Free-tier `nvapi-` key from [build.nvidia.com](https://build.nvidia.com/settings/api-keys) |
| Ollama host setup | [Ollama host runbook](gen3-admin/ollama-host-setup) — install, pull `embeddinggemma`, LAN URL |
| Ollama discovery | Discover models on your Ollama provider in **Models** |
| Discover models | Confirm Groq + NIM models appear |
| Platform defaults | **Required:** embedding, LLM, helper (+ web search when enabled) |
| Model pricing | Review $0 free-tier pricing rows |
| Compound verify | Enable Groq Compound for web-search agents |
| Users | Create or bulk-upload at least one `tenant_owner` |
| SMTP | Configure email or skip with acknowledgment |
| Helper settings | Confirm GT Helper model |
| Paid providers (optional) | Add OpenAI/Anthropic later — not required |
| Complete | Summary and next steps |

## CLI baseline (optional)

Before opening the UI, operators may apply the universal baseline from the cluster:

```bash
gt-ai-os-admin setup-baseline-apply --namespace <namespace> --yes
```

Then finish personalization in QuickStart.

## Related articles

- [Getting Started](gen3-admin/getting-started)
- [Models](gen3-admin/models)
- [Ollama host setup](gen3-admin/ollama-host-setup)
- [Users](gen3-admin/users)
- [Email Settings](gen3-admin/email-settings)
