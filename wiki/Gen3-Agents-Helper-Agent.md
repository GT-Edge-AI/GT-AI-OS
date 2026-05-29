# GT Helper

## Start Here

1. Look for the **?** bubble fixed on the tenant shell (lower-right on most pages).
2. Click **?** to open the **GT Helper** help shelf—a hybrid panel with **Search instructions**, **Suggested for this page**, and **Ask GT Helper** chat.
3. Search the wiki or click **Open page instructions** for the article suggested for your current route.
4. Type a substantive question in **Ask GT Helper** when you want conversational guidance grounded in wiki excerpts for your role.
5. Follow `[route: /path|Label]` links in numbered steps and `[slug: gen3/...]` citations at the end of answers into the **Instructions** drawer for full articles and screenshots.
6. Open the **Instructions** drawer from the account menu (**GT AI OS Instructions**) or **Full instructions** inside the help shelf when you want browse-and-read mode instead of chat.

![Tenant GT Helper help shelf with search, page suggestion, and Ask GT Helper](gen3/images/instructions-help-shelf.png)

## Why this matters

**GT Helper** is the fastest way to get **tenant-specific, conversational guidance** without leaving GT AI OS. It complements the wiki corpus: use the **Instructions** drawer (book icon / account menu) for stable procedures and screenshots, and use the **?** help shelf when you want interactive “what should I click next?” answers scoped to what your role can actually access.

GT Helper is **not** a favorited agent on the [Agents](gen3/agents) page and does not appear in **Favorite Agents** or **Agent Configuration**. It is a built-in instructions assistant backed by the tenant wiki corpus.

## Details

### Two ways to reach instructions

| Surface | How to open | Best for |
| --- | --- | --- |
| **? help shelf (GT Helper)** | Fixed **?** bubble on the tenant shell | Search, page suggestions, and **Ask GT Helper** chat on the page you are on |
| **Instructions drawer** | Account menu → **GT AI OS Instructions**, or **Full instructions** in the help shelf | Browsing the wiki tree, reading full articles, screenshots, and role-filtered navigation |

The help shelf and Instructions drawer share the same wiki corpus, but only the help shelf runs passive retrieval and **Ask GT Helper** chat.

### What the help shelf includes

The hybrid shelf has three regions:

- **Search instructions** — keyword search across wiki articles your role can see.
- **Suggested for this page** — opens the article best matched to your current route (**Open page instructions**).
- **Ask GT Helper** — multi-turn chat grounded in wiki excerpts, with prior threads in the side rail (**New question**, thread search, and time filter).

### How answers are built

GT Helper uses a two-stage retrieval and generation pipeline.

#### 1. Passive retrieval (every substantive question)

Before the model replies, the tenant API gathers role-filtered wiki excerpts:

1. **Corpus filter** — articles are limited to your **tenant role** and **GT API enablement** (`gtApiEnabled`). GT API articles are hidden when GT API is off for your account.
2. **Keyword match** — title and body are scored against your question (token matching with synonym expansion).
3. **Route and topic injection** — articles tied to your current page path and detected question topics are injected even when keyword scores are weak.
4. **Hybrid rank** — candidates are merged with:
   - keyword score
   - route boost for page-relevant slugs
   - **title embedding similarity** (query embedding compared to cached article-title vectors on the tenant)

Excerpt limits depend on role: tenant users receive up to 12 excerpts; tenant owners and managers receive up to 20.

Passive excerpts are injected into the model system context as starting evidence. They may be incomplete.

#### 2. Agentic search (when excerpts are not enough)

When passive excerpts are missing or insufficient for a **GT AI OS product** question, the model may call the **`search_instructions_wiki`** tool with a focused query (optional `pagePath` and `limit`).

- **`search_instructions_wiki`** searches the **instructions wiki corpus** for product documentation. It is **not** the same as an agent's **`web_search`** tool, which queries the public internet during **GT Chat** when web search is enabled on that agent.

- On the **tenant app**, tool execution is routed through the **resource cluster**, which forwards the search to the tenant instructions API and returns article excerpts to the model.
- The chat loop continues across tool rounds until the model produces a final answer or hits provider round limits.

Casual messages (see below) skip both passive retrieval and tool calls.

### Grounding policy

GT Helper follows a strict split between product behavior and general knowledge.

| Question type | Source | Behavior |
| --- | --- | --- |
| **GT AI OS product behavior** — screens, routes, roles, workflows, settings, in-app affordances | Instructions wiki only | Answer from wiki excerpts, `search_instructions_wiki` results, and factual current-page UI context. **Do not invent** features, navigation, policies, or steps. |
| **General knowledge** — OIDC/SAML theory, markdown syntax, industry concepts not specific to this product's UI | General knowledge allowed | Answer from general knowledge; **clearly separate** from GT AI OS-specific guidance. |
| **Mixed questions** | Both | Use general knowledge for the non-product portion; use wiki-backed guidance for the GT AI OS portion. |
| **Missing wiki evidence** for a product question | None sufficient | State what is missing. Suggest opening the **Instructions** drawer or asking a narrower question (or a focused `search_instructions_wiki` query via a rephrased **Ask GT Helper** prompt). Do not guess product behavior. |

Numbered GT AI OS steps are provided only when each step is supported by excerpts, tool results, or page UI context.

### Citations and links

GT Helper formats in-app navigation for the UI to render as clickable links:

- **`[route: /path|Label]`** — one marker per page reference inside **numbered steps**. Example: `[route: /datasets|Datasets]`.
- **`[slug: gen3/...]`** — one primary-source citation at the **end** of the answer, not after every step.

Duplicate route or slug markers in a single answer are suppressed during normalization.

### Access gates

| Gate | Effect on GT Helper |
| --- | --- |
| **Tenant role** | Wiki corpus and answers are scoped to articles your role can reach. The helper will not describe routes or admin pages you cannot open. |
| **GT API disabled** (`gtApiEnabled` false) | GT API wiki articles are excluded from search, suggestions, and chat context. |
| **Read-only account** (`accountReadOnly` true) | The helper does not describe create, edit, import, or delete actions. |

Authorization is not bypassed—if your role cannot access a feature, GT Helper cannot grant it.

### Casual messages

Short greetings and small talk (for example **hi**, **thanks**, **good morning**) receive a **brief reply** in one or two sentences. GT Helper does **not** run passive retrieval or wiki search until you ask a **substantive product question**.

Messages that contain help phrasing (`how do`, `what is`, `where is`, `help me`, etc.) or product terms (`dataset`, `agent`, `policy`, etc.) are treated as substantive even when short.

### Multi-turn threads

**Ask GT Helper** maintains conversation history (up to 20 prior messages in context). Continuing threads:

- answer only the latest user message
- resolve pronouns (`it`, `them`, `that`, `there`) from earlier turns
- avoid repeating greetings or re-introducing itself

Thread titles are derived from your first substantive question, optionally suffixed with the current page or primary documentation hit. Prior threads appear in the help shelf thread rail.

### Configuration (operator)

GT Helper chat requires a deployment-wide default model:

- Super Admins set **Default GT Helper model** (`defaultInstructionsHelperModelId`) on Control Panel **Models → Default Models**.
- When unset or invalid, **Ask GT Helper** returns **503 Service Unavailable** with a configuration error asking operators to set the default.

See [GT Helper (Control Panel)](gen3-admin/instructions-helper) for the operator-side help shelf and [Models](gen3-admin/models) for default model administration.

### Observability

All signed-in tenant roles can open [Observability](gen3/observability). Use the **GT Helper (Tenant)** tab for help-shelf usage:

- **Usage** — threads, messages, inference and embedding tokens, top cited wiki topics, top users (when your role allows user filtering), and settled billing when exposed.
- **Threads** — searchable helper transcripts with page path, model, token counts, and source slugs per turn.

This tab covers tenant **?** shelf traffic only. It does **not** include Control Panel GT Helper / CTP Helper traffic.

Inference and embedding burn is tagged with `requestMode=instructions_helper`.

### Tips for good prompts

- Name the workspace you are in (“I am on Datasets—how do I share with a group?”).
- Ask for numbered steps when you want a checklist.
- Follow `[route:…]` and `[slug:…]` citations into the Instructions drawer for screenshots and RBAC notes.
- Rephrase narrowly if the helper reports missing wiki evidence.

### What GT Helper is not

- A replacement for tenant policy, compliance text, or Control Panel operator settings.
- A favorited chat agent on the [Agents](gen3/agents) page.
- A bypass for authorization or read-only account restrictions.

### Related pages

- [Agents](gen3/agents)
- [Getting Started](gen3/getting-started)
- [Observability](gen3/observability)
- [Getting Support](gen3/getting-support)
- [How to Build Your AI Workflow](gen3/workflows)
- [GT Helper (Control Panel)](gen3-admin/instructions-helper) — operator documentation for the Control Panel help shelf
