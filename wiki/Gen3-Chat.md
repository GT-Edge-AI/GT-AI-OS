# GT Chat

## Start Here

1. Open **GT Chat** and select an agent.
2. Attach datasets or upload files if the task needs source material.
3. Wait for document processing to finish before the next prompt when uploads are pending.
4. Send your prompt and review the streamed response.
5. Use copy, download, or report actions on assistant messages when needed.

![Paperclip and dataset attachment in chat](gen3/images/chat-paperclip.png)

## Why this matters

GT Chat is the live execution surface—agent, conversation, datasets, uploads, and streaming answers in one workspace.

## Details

`GT Chat` is the live execution surface for the current Gen 3 tenant app. It combines the selected agent, the current conversation transcript, any conversation-attached datasets, staged uploads, and the assistant response stream in one workspace.

## What the active GT3 chat page does

- starts new conversations
- reopens recent conversations from the chat sidebar
- launches chat from an agent card or favorite agent
- attaches existing datasets to the current conversation
- uploads files into a chat-created or user-selected dataset
- shows response actions such as copy, download, and report

Conversation history still exists outside chat, but the dedicated history route is [Conversations](gen3/conversations), not a separate documents or workflow page.

### Dataset retrieval vs web search in chat

Favorited agents may call **`search_datasets`** when conversation or agent datasets provide scope—that tool retrieves from **your tenant corpora**, not the public internet. **`web_search`** is a separate managed tool for live public-web research and requires deployment defaults plus per-agent web search settings (see [Building Agents](gen3/agents/building)). Do not expect current-events answers from dataset retrieval alone.

## Standard chat workflow

1. Choose an agent.
2. Confirm whether that agent already brings its own default datasets.
3. Add any extra datasets or upload files for this conversation.
4. Send your prompt.
5. Wait for uploads to finish processing if the chat shows pending document ingestion.
6. Review the assistant response and use copy, download, or report actions when needed.

## Understanding the main chat controls

### Agent selector

Every conversation runs through a selected agent. You can arrive in chat from the direct `/chat` route, or by opening chat from [Agents](gen3/agents). If you need a different behavior profile, switch agents before sending the next prompt.

### Datasets panel

The **Add Datasets to Conversation** panel lets you attach existing datasets or upload new files into a dataset. Use it when the current conversation needs retrieval from specific source material.

### Conversation history rail

The chat sidebar keeps recent conversations close to the live workspace. Use it for quick switching. Move to [Conversations](gen3/conversations) when you need broader search, filtering, or exports across many threads.

### Assistant message actions

Completed assistant messages can expose:

- **Copy** to place the rendered answer on your clipboard
- **Download** to export the conversation content in supported formats
- **Report** to capture the prompt/response pair for support investigation

## Working safely with uploads

Uploaded files do not become instantly searchable. Gen 3 blocks the next message until the staged files finish processing into the target dataset. If you upload files and the composer remains disabled, wait for the processing indicator to clear before sending the next prompt.

## When to leave GT Chat for another page

| Need | Best page |
| --- | --- |
| Build or edit the agent itself | [Agents](gen3/agents) |
| Bulk-manage datasets and documents | [Datasets](gen3/datasets) |
| Search or export older threads | [Conversations](gen3/conversations) |
| Review usage or access analytics | [Observability](gen3/observability) |

## Best practices

- Keep one conversation focused on one line of work when you expect to export or review it later.
- Attach only the datasets you actually need so retrieval scope stays predictable.
- Use agent defaults for repeatable work and conversation-attached datasets for one-off context.
- Report bad outputs from the message that demonstrates the issue instead of describing the problem from memory later.

## Learn more

- [Starting Conversations](gen3/chat/starting-conversations)
- [Using Datasets in Chat](gen3/chat/using-datasets)
- [Reviewing and Exporting Conversations](gen3/chat/reviewing-conversations)
