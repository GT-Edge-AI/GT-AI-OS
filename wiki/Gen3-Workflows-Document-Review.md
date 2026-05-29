# Document Review Workflow

## Start Here

1. Create a [dataset](gen3/datasets) for the documents you want to review together.
2. Upload your documents to that dataset ([Uploading and Importing Documents](gen3/datasets/uploading)).
3. Open [GT Chat](gen3/chat) and select an agent configured for **document Q&A** or RAG over datasets.
4. Select the **paperclip** in the chat message bar at the bottom of the screen.
5. Select the dataset you want the agent to reference for this conversation.
6. Send a prompt and ask questions about the documents in that dataset.

![Paperclip control in GT Chat for attaching a dataset](gen3/images/chat-paperclip.png)

## Why this matters

Document review is one of the most common tenant workflows: operators need repeatable retrieval over a bounded corpus, not one-off pasted text. Datasets hold the source material; agents define how answers are formed; chat attaches the right dataset scope per conversation so retrieval stays predictable.

## Details

### Before you start

- Confirm documents finished processing in the dataset (pending ingestion blocks the next chat message).
- If answers miss content, check [Managing Dataset Content](gen3/datasets/managing) and the agent’s default dataset attachments in [Building Agents](gen3/agents/building).

### Agent selection

Use an agent intended for document Q&A—one with dataset/RAG instructions and retrieval tuning. Generic chat agents may work but often produce weaker citations and less predictable retrieval over uploaded files.

### Attaching datasets in chat

The paperclip opens **Add Datasets to Conversation**. You can attach multiple datasets when the review spans collections; keep scope minimal so citations and retrieval stay focused.

### Prompt patterns

- Ask for summaries, comparisons, or gap analysis across uploaded files.
- Reference document types explicitly (“compare the SOP PDF to the checklist DOCX”).
- Use [Reviewing and Exporting Conversations](gen3/chat/reviewing-conversations) when you need an audit trail of the review thread.

### When to use GT API instead

When GT API is enabled for your account, automation pipelines (scheduled ingestion, external tools) should use [GT API](gen3/gt-api/overview) dataset upload keys and published agent aliases rather than manual chat uploads.

### Related workflows

- [Diagram Review](gen3/workflows/diagram-review)
- [Mock Assessments](gen3/workflows/mock-assessments)
- [Using Datasets in Chat](gen3/chat/using-datasets)
