# How to Build Your AI Workflow

## Start Here

1. Read [Getting Started](gen3/getting-started) to see which workspaces your role can access.
2. Pick a workflow guide below that matches your goal.
3. Prepare [Datasets](gen3/datasets) and [Agents](gen3/agents) before opening [GT Chat](gen3/chat).
4. For external tools, plan a [GT API](gen3/gt-api/overview) rollout (requires **GT API enabled** on your account) instead of manual chat steps.
5. Use the **?** help shelf ([GT Helper](gen3/agents/helper-agent)) when you want conversational guidance inside the app.

![Tenant Help shelf for workflow guidance](gen3/images/instructions-help-shelf.png)

## Why this matters

GT AI OS is flexible; most failures come from skipping setup (no dataset, wrong agent, missing paperclip attachment). These workflow articles give **repeatable sequences** for the use cases operators ask about most—document review, diagram review, and mock assessments—using the same Gen 3 routes you already have in the tenant app.

## Details

### Workflow guides

| Goal | Article |
| --- | --- |
| Review text documents with retrieval | [Document Review](gen3/workflows/document-review) |
| Review diagrams and visual artifacts | [Diagram Review](gen3/workflows/diagram-review) |
| Run training or evaluation exercises | [Mock Assessments](gen3/workflows/mock-assessments) |

### Core building blocks

- **Agents** — behavior, model choice, default datasets ([Agents](gen3/agents), [Building Agents](gen3/agents/building)).
- **Datasets** — durable source material ([Datasets](gen3/datasets)).
- **GT Chat** — live execution with paperclip dataset attachment ([GT Chat](gen3/chat)).
- **GT API** — OpenAI-compatible automation ([GT API Overview](gen3/gt-api/overview)).

### Structured automation elsewhere

The tenant route `/workflows` (when enabled in your deployment) may expose multi-step automation definitions separate from these instructional guides. Use chat for exploratory work; use workflow automation when your tenant ships repeatable orchestration in that workspace.

### Related pages

- [Using Datasets in Chat](gen3/chat/using-datasets)
- [Conversations](gen3/conversations) — review and export completed workflow threads
