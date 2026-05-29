# GT AI OS Instructions Wiki Authoring Guide

This wiki currently serves both Gen 2 and Gen 3 during the migration period.

## Index files

- `_index.json` keeps the live Gen 2 tenant navigation
- `_super-admin-index.json` keeps the live Gen 2 control-panel navigation
- `_gt3-index.json` is the Gen 3 tenant navigation
- `_gt3-super-admin-index.json` is the Gen 3 control-panel navigation

## Naming rules

- `getting-started` is a special legacy slug that maps to `Home.md`
- other slugs flatten into a single wiki filename
- example: `agents/creating` becomes `Agents-Creating.md`
- example: `gen3/chat/using-datasets` becomes `Gen3-Chat-Using-Datasets.md`

Slug generation matches `gt-ai-os/internal/shared/instructions/wiki.go` (`SlugToWikiFilename`): each path segment is title-cased and joined with hyphens, e.g. `gen3/gt-api/overview` → `Gen3-Gt-Api-Overview.md` at repo root.

## Gen 3 page template (required)

Every `Gen3*.md` and `Gen3-Admin*.md` article uses this structure:

```markdown
# Page Title

## Start Here

1. First concrete step (UI control names in **bold**).
2. …

## Why this matters

One or two short paragraphs on outcome and when to use this page.

## Details

Existing reference content, tables, and deep dives live here.
```

**Start Here** steps must be page-specific and actionable (not generic placeholders). **Why this matters** explains value. **Details** preserves or reorganizes prior body content—do not delete operational depth when restructuring.

## Images

- Tenant articles: place assets under `gen3/images/` (e.g. `gen3/images/chat-paperclip.png`).
- Control Panel articles: place assets under `gen3-admin/images/` (e.g. `gen3-admin/images/cp-models.png`).
- Markdown syntax: `![descriptive alt text](gen3/images/filename.png)` for tenant pages, or `![descriptive alt text](gen3-admin/images/filename.png)` for Control Panel pages. From an article in the same namespace you may also use `./images/filename.png` (resolved to `gen3/images/…` or `gen3-admin/images/…` via `WikiAssetURL`). Alt text is required for accessibility.
- Paths are wiki-relative; the tenant and Control Panel apps resolve them against the article namespace via `WikiAssetURL`.

### Captured screenshot filenames (RKE2 local)

Placeholder PNGs may ship in the repo until operators replace them with RKE2 captures. Keep filenames stable so markdown embeds stay valid.

| File | Use on |
| --- | --- |
| `gen3/images/sidebar-expanded.png` | [Getting Started](gen3/getting-started) — expanded sidebar, Agents submenu, Management dropdown |
| `gen3/images/sidebar-collapsed-rail.png` | [Getting Started](gen3/getting-started) — collapsed rail with flattened management icons |
| `gen3/images/chat-paperclip.png` | [GT Chat](gen3/chat), [Using Datasets in Chat](gen3/chat/using-datasets), workflow pages that attach datasets |
| `gen3/images/agents-favorites.png` | [Agents](gen3/agents) favorites flow |
| `gen3/images/agents-create-tabs.png` | [Building Agents](gen3/agents/building) — Agent Configs vs Agent Templates tabs |
| `gen3/images/agents-templates-catalog.png` | [Building Agents](gen3/agents/building) — template catalog cards |
| `gen3/images/agents-template-applied.png` | [Building Agents](gen3/agents/building) — template applied banner |
| `gen3/images/agents-web-search-tab.png` | [Building Agents](gen3/agents/building) — Web Search Settings tab |
| `gen3/images/model-catalog.png` | [Model Catalog](gen3/model-catalog) |
| `gen3/images/gt-api-overview.png` | [GT API Overview](gen3/gt-api/overview) |
| `gen3/images/gt-api-keys.png` | [GT API Keys and Access](gen3/gt-api/keys-and-access) |
| `gen3/images/gt-api-published-endpoints.png` | [GT API Published Endpoints](gen3/gt-api/published-endpoints) |
| `gen3/images/gt-api-openai-compatibility.png` | [GT API OpenAI Compatibility](gen3/gt-api/openai-compatibility) |
| `gen3/images/observability-helper-tab.png` | [Observability](gen3/observability) — GT Helper (Tenant) tab |
| `gen3/images/instructions-help-shelf.png` | Tenant **?** help shelf ([GT Helper](gen3/agents/helper-agent), [Getting Started](gen3/getting-started), [Workflows](gen3/workflows)) |
| `gen3/images/instructions-rbac-badge.png` | Role-gated wiki links in the Instructions drawer |
| `gen3-admin/images/cp-models.png` | Control Panel [Models](gen3-admin/models) |
| `gen3-admin/images/cp-default-models-web-search.png` | [Models](gen3-admin/models) — Default Models web search section |
| `gen3-admin/images/cp-help-shelf.png` | Control Panel **?** help shelf ([GT Helper](gen3-admin/instructions-helper), [Instructions Settings](gen3-admin/instructions-settings)) |
| `gen3-admin/images/cp-helper-usage.png` | [CTP Helper Usage](gen3-admin/helper-usage) |
| `gen3-admin/images/cp-updates.png` | [Updates](gen3-admin/updates) |
| `gen3-admin/images/cp-backup-restore.png` | [Backup & Restore](gen3-admin/backup-restore) |

Replace files in place when refreshing captures; do not rename without updating every embed.

### Agent template CSV assets

Curated agent starters live in the instructions repo under `agent-templates/*.csv` (for example `document-chat-agent.csv`). The tenant **Agent Templates** tab lists these files via GitHub through the tenant API; authors add or edit CSVs there—not under `gen3/images/`. Document template behavior in [Building Agents](gen3/agents/building).

## RBAC, GT API gate, and links

- Navigation `role` in `_gt3-index.json` / `_gt3-super-admin-index.json` controls drawer visibility (`all`, `tenant_manager`, `tenant_owner`, legacy `admin` → owner).
- **`role: all`** means every signed-in tenant role may see the nav entry. **`tenant_manager`** means tenant managers and tenant owners (owner level ≥ manager level). **`tenant_owner`** (or legacy `admin`) is owner-only.
- **Observability** uses `role: all` in `_gt3-index.json` because every signed-in role can open `/observability`. Article copy must still document **per-role tabs and scope** (owners see billing; managers do not; API tab requires `gtApiEnabled`).
- **Users** uses `role: tenant_manager` because both tenant managers and tenant owners see the sidebar item; tenant users do not.
- **GT API** (`gen3/gt-api/*`) entries stay `role: all` in the index, but the tenant app **also** requires **`gtApiEnabled`** on the session. When GT API is disabled, sidebar `/gt-api`, observability **API** tab, instructions drawer GT API section, and helper corpus hits for `gen3/gt-api/...` are hidden. Document this prerequisite in GT API articles and anywhere integrations are mentioned.
- For restricted topics, **prefer wiki links** such as `[Observability](gen3/observability)` in prose so the UI can badge links the reader may not be allowed to open inline (`slugRoles` metadata).

![Role badge on a wiki link the reader cannot open](gen3/images/instructions-rbac-badge.png)
- Do not instruct users to bypass role gates or capability flags; tell them to confirm role, GT API enablement, or contact a tenant owner/manager.

## Instructions helper (? bubble)

- Gen 3 help is **not** a favorited chat agent. The tenant and Control Panel shells expose a fixed **?** bubble (`instructions-help-fab`) that opens a **hybrid help shelf**: wiki search, a route-based page suggestion, and **Ask helper** chat.
- Product name in indexes and user-facing copy: **GT Helper**. Tenant wiki: `Gen3-Agents-Helper-Agent.md` / slug `gen3/agents/helper-agent` (`_gt3-index.json` child title **GT Helper**). Control Panel wiki: slug `gen3-admin/instructions-helper` (`_gt3-super-admin-index.json` title **GT Helper**). Prose may say **? help shelf**; do not instruct users to favorite a helper agent.
- **Grounding policy for authors:** For GT AI OS product behavior (screens, routes, roles, policies, workflows, settings), the wiki is the authoritative source. Write steps and affordances that actually exist in the app; do not invent navigation or policies the corpus does not support. General industry background (generic OIDC theory, markdown syntax, etc.) may appear in articles when clearly separated from product-specific steps. If an article is thin on a topic, expand the wiki rather than expecting the helper to guess.
- **Retrieval:** The helper passively ranks role-filtered wiki excerpts (keyword + embedding hybrid) and may call `search_instructions_wiki` for additional excerpts. Tenant corpus limits vary by role (~12 excerpts for tenant users, ~20 for managers/owners). Control Panel helper uses the `gen3-admin/...` corpus. Match [RBAC](#rbac-gt-api-gate-and-links) and GT API gates so retrieved text aligns with what readers can open.
- **Citation conventions** (model output; authors should know how answers link back):
  - `[route: /path]` or `[route: /path|Label]` — one clickable in-app route per page reference in numbered steps; do not duplicate the same path in plain text or markdown links in the same answer.
  - `[slug: gen3/...]` or `[slug: gen3-admin/...]` — primary source article at the end of the answer (not after every step).
  - The UI deduplicates repeated markers; prefer stable slugs from `_gt3-index.json` / `_gt3-super-admin-index.json`.
- The backend filters wiki excerpts by **tenant role** and **`gtApiEnabled`** on the tenant app (`FilterTenantWikiNav`). Author copy should match what each role can actually open—do not describe owner-only or GT API routes as universally available.

## Cross-linking to in-app routes

When documenting tenant UI that maps to a route, mention the workspace and link wiki slugs:

| Workspace | Wiki slug prefix | In-app path (tenant) | Sidebar placement | Extra gate |
| --- | --- | --- | --- | --- |
| GT API | `gen3/gt-api/...` | `/gt-api` | Top-level (between **Conversations** and **Management**) | `gtApiEnabled` |
| GT Chat | `gen3/chat/...` | `/chat` | Launch from agents / history (not top-level nav) | — |
| Agents | `gen3/agents/...` | `/agents` | Top-level with submenu | — |
| Datasets | `gen3/datasets/...` | `/datasets` | Top-level | — |
| Conversations | `gen3/conversations/...` | `/conversations` | Top-level | — |
| Observability | `gen3/observability` | `/observability` | **Management → Observability** | Per-role tabs |
| Users | `gen3/users` | `/users` | **Management → Users** | `tenant_manager` or `tenant_owner` |
| Groups | `gen3/groups/...` | `/groups` | **Management → Groups** | — |
| Model Catalog | `gen3/model-catalog` | `/model-catalog` | **Management → Model Catalog** | — |
| Account Settings | `gen3/settings` | `/settings` | Account menu (**Settings** / **Profile**) | Owner edits policy |
| Instructions | `gen3/...` | — | Account menu **GT AI OS Instructions** + **?** shelf | Role + GT API corpus filter |

**Collapsed rail note:** When the sidebar is collapsed, **Management** routes appear as individual rail icons (not a nested **Management** button). Expanded mode uses the **Management** dropdown.

Use wiki links in markdown for instructions navigation; use plain path text (`/gt-api`) when telling users where to click in the app shell.

## Migration rule

Do not delete or rename live Gen 2 pages while Gen 2 consumers are still active. Add Gen 3 pages and index updates in parallel, then retire Gen 2 content in a later cleanup phase.

## Publishing

Content changes in this repo are consumed by GT AI OS via the configured wiki raw URLs. Coordinate with operators before pushing to GitHub when deployment pins a specific wiki revision.
