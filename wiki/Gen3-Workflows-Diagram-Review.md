# Diagram Review Workflow

## Start Here

1. Create a dataset for diagram source files ([Datasets](gen3/datasets))—PNG, PDF pages, Visio exports, or other supported diagram formats.
2. Upload diagrams to the dataset and wait for processing to complete ([Uploading and Importing Documents](gen3/datasets/uploading)).
3. Open [GT Chat](gen3/chat) and choose an agent with **vision** or diagram-review instructions (or another agent tuned for spatial and labeling questions).
4. Use the **paperclip** to attach the dataset containing your diagrams.
5. Ask specific questions: component identification, data-flow checks, legend validation, or compliance against a written standard.

![Paperclip in chat for dataset attachment during diagram review](gen3/images/chat-paperclip.png)

## Why this matters

Diagrams are not plain text—effective review requires vision-capable models and agents tuned for spatial and labeling questions. Keeping diagrams in a dataset lets you reuse the same corpus across multiple review sessions and share it with collaborators through [Groups](gen3/groups).

## Details

### Dataset and vision settings

- When creating datasets that rely on image understanding, confirm vision or multimodal settings in [Datasets](gen3/datasets) and agent configuration ([Building Agents](gen3/agents/building)).
- Large blueprints may need to be split into readable pages or tiles before upload.

### Chat practices

- Reference diagram names or page numbers in prompts.
- Ask the agent to list assumptions when labels are ambiguous.
- For side-by-side comparisons, attach datasets that contain both versions and ask for a structured diff.

### Collaboration

Share the dataset or agent with a [Group](gen3/groups) when multiple reviewers need the same diagram corpus. Use [Conversations](gen3/conversations) to export review threads for records.

### External automation

For bulk diagram ingestion from tools, use [GT API](gen3/gt-api/overview) upload keys and chat aliases when GT API is enabled for your account, instead of manual paperclip attachment.

### Related workflows

- [Document Review](gen3/workflows/document-review)
- [Mock Assessments](gen3/workflows/mock-assessments)
