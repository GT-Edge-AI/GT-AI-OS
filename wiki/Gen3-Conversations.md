# Conversations

## Start Here

1. Open **Conversations** from the tenant sidebar.
2. Search or filter for the thread you need.
3. Reopen a conversation into **GT Chat** or export when supported.
4. Use exports for records management after significant workflows.

## Why this matters

Conversation history is the system of record for what the agent said, when, and under which agent configuration.

## Details

`Conversations` is the active Gen 3 history workspace. Use it when you need to search across stored threads, filter by agent or dataset, inspect a conversation outside the live chat route, or export history in bulk.

## What the page supports

- searching titles and message content
- filtering by agent, dataset, and time window
- reviewing the selected conversation transcript
- reopening a conversation in [GT Chat](gen3/chat)
- exporting filtered history as JSON or DOCX
- exporting an individual conversation as JSON or DOCX

## How it differs from GT Chat

Use [GT Chat](gen3/chat) for active work. Use `Conversations` when the work is complete and you need to find, compare, review, or export prior threads.

## Standard review workflow

1. Open `Conversations`.
2. Enter a search term if you know part of the title or a message phrase.
3. Narrow the list with agent, dataset, or time filters.
4. Select the conversation you want to inspect.
5. Export it or reopen it in chat if you need to continue the thread.

## Filters and exports

### Search

Search checks conversation titles and message text, so it is the best first step when you remember content but not the exact thread name.

### Agent and dataset filters

These filters help when you want to review only the work associated with a specific agent or the dataset-backed conversations for a particular knowledge source.

### Time filter

Use time filtering to isolate recent activity such as `Today`, `This week`, or `This month` before exporting or reviewing.

### Export formats

- **JSON** is best for machine-readable archival or downstream processing
- **DOCX** is best for a human-readable document handoff

## Message-level actions

Within the selected conversation detail view, Gen 3 keeps the same practical response actions exposed in live chat:

- copy individual message content
- download the conversation
- move back into the live chat workspace when the thread should continue

## Best practices

- Apply filters before bulk export so the output matches a real business question.
- Prefer reopening the exact conversation in chat instead of starting over when context continuity matters.
- Export a single conversation when you need one clean handoff, and use filtered exports for reporting or audit packets.

## Related pages

- [GT Chat](gen3/chat)
- [Reviewing and Exporting Conversations](gen3/chat/reviewing-conversations)
- [Observability](gen3/observability)
