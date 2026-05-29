# Using Datasets in Chat

## Start Here

1. Open **GT Chat** for the conversation you are extending.
2. Select the **paperclip** in the message composer.
3. Choose existing datasets or upload into a dataset from the panel.
4. Wait for processing to complete if files were uploaded.
5. Ask questions that reference the attached corpus.

![Paperclip control for dataset attachment](gen3/images/chat-paperclip.png)

## Why this matters

Dataset attachment binds retrieval scope to the conversation so answers cite the material you intended—not the entire tenant library.

## Details

Datasets are the active Gen 3 retrieval context for chat. A conversation can use datasets in two ways: through the selected agent's default dataset configuration, or through datasets you attach directly to the conversation.

## The two dataset paths

### Agent-attached datasets

Some agents bring default datasets with them. Use this when the same knowledge sources should always travel with the agent.

### Conversation-attached datasets

Use the **Add Datasets to Conversation** panel when the retrieval context is specific to the current thread and should not change the agent for every future user.

### Dataset retrieval vs web search

- **`search_datasets`** — searches attached datasets and staged uploads in the current conversation. Use when answers must come from documents you control.
- **`web_search`** — searches the public web through the managed web search model. Use when the task needs current or external public facts. Requires agent and deployment web search gates; it does **not** replace dataset attachment for private corpora.

If an agent lacks web search configuration, ask for sources inside attached datasets or enable web search on the agent before expecting live web citations.

## Uploading files from chat

Gen 3 also lets you upload files from the chat dataset panel. Those files are ingested into:

- a chat-created upload dataset when you keep the automatic upload target
- or a dataset you choose explicitly

This is useful when you need one-off working material without leaving the chat workflow.

## Recommended chat dataset workflow

1. Choose the agent.
2. Open the dataset panel.
3. Attach the datasets already needed for the task.
4. Upload additional files only if the existing datasets are incomplete.
5. Wait for processing to finish before sending the next message.

## When to use chat uploads vs the Datasets page

| Situation | Best path |
| --- | --- |
| You need quick one-off files for the current conversation | Upload from chat |
| You are building or cleaning a reusable knowledge source | Use [Datasets](gen3/datasets) |
| You need to control sharing, metadata, or retrieval defaults carefully | Use [Datasets](gen3/datasets) |

## Best practices

- Attach only the datasets needed for the question.
- Keep reusable source material in named datasets instead of leaving everything in chat-created upload datasets.
- Re-check attached datasets after switching agents, because the active retrieval set may have changed.
- If a result seems ungrounded, verify the attached datasets before editing the prompt.

## Troubleshooting

### The send button is disabled after upload

The files are still processing. Wait until chat no longer reports pending attachment ingestion.

### The assistant is not using the expected documents

- confirm the target dataset is attached
- confirm the files finished processing successfully
- confirm the needed files are actually in the dataset by reviewing [Datasets](gen3/datasets)

### A dataset should be reusable by others

Move the work into a managed dataset on [Datasets](gen3/datasets) and apply the correct sharing posture instead of relying on a temporary chat upload path.

## Related pages

- [Datasets](gen3/datasets)
- [Managing Dataset Content](gen3/datasets/managing)
- [Agents](gen3/agents)
