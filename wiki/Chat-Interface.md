# Chat Interface

The chat interface is your primary way of interacting with AI agents in GT AI OS.

## Quick Links

- [Managing Conversations](chat-interface/managing-conversations) - History, search, and organization
- [Using Datasets in Chat](chat-interface/using-datasets) - Add documents to conversations

## Selecting an Agent

### From the Agents Page (Recommended)

1. Go to **Agents** in the sidebar (opens **Favorite Agents** view)
2. Click any agent card to start a conversation immediately
3. To browse all agents, click the toggle in the top right to switch to **Agent Configuration** view

### Browsing by Category

Agents are organized by category to help you find what you need. Use the category and tag filters on the Agents page to narrow down your search.

Common category examples:
- **General Purpose** - Research, writing, brainstorming
- **Technical** - Code review, debugging, architecture
- **Domain Expert** - Specialized knowledge areas
- **Creative** - Content creation, copywriting

### Switching Agents

To use a different agent:

1. Click the **Bot icon** (to the left of the message input box)
2. This takes you to the Agents page
3. Select a new agent to begin a fresh conversation

**Note**: Switching agents exits your current conversation. You can resume it later from the conversation history.

### Starting a New Chat (Same Agent)

To start a fresh conversation with the same agent:
- Click **New Chat** in the top-right corner of the header

## Current Agent Display

The currently selected agent name is displayed in the header at the top of the chat interface. This helps you confirm which agent you're chatting with.

## Adding Datasets

Agents can access your documents in two ways:

### Agent-Configured Datasets
Datasets can be attached to an agent permanently in the agent's configuration. These datasets are available in all conversations with that agent.

### Conversation Datasets
You can also add datasets to a specific conversation:

1. Click the **Paperclip icon** (to the left of the message input)
2. Either upload new files or select existing datasets
3. The agent can search selected datasets for relevant information

See [Using Datasets in Chat](chat-interface/using-datasets) for details.

## Easy Buttons

Some agents have **Easy Buttons** - quick-access prompts that appear as clickable buttons in the chat interface. Click any Easy Button to send that prompt instantly.

Easy Buttons are configured by the agent creator. See [Creating Agents](/agents/creating) for details on setting them up.

## Message Features

### Rich Text Responses

Agents respond with formatted text including:
- Headers and text styling
- Bulleted and numbered lists
- Code blocks with syntax highlighting
- Tables for structured data

### Code Blocks

Code responses include syntax highlighting and a copy button:

```python
def greet(name):
    return f"Hello, {name}!"
```

## Downloading Chat Content

You can download chat messages for reference or sharing. Hover over any agent message to see the **Download** button.

### Download Options

**Response Only** (default)
- Downloads only the current agent message
- Optional: Check "Include Last User Prompt" to include your question

**Entire Conversation**
- Toggle to "Conversation" mode in the dropdown
- Downloads all messages in the conversation

### Available Formats

| Format | Best For |
|--------|----------|
| TXT | Plain text, basic sharing |
| MD | Preserves markdown formatting |
| DOCX | Editable Word documents |
| CSV | Tables and spreadsheet data |

### Downloading Tables

If a response contains tables and you select **CSV** format:
- If multiple tables exist, choose which table(s) to download
- Select "All Tables" to combine them in one file

## Reporting Chat Issues

If an agent response is problematic, you can report it for review.

### How to Report

1. Hover over the agent message with the issue
2. Click the **Report Chat Issue** button (flag icon)
3. Select the type of issue:
   - Harmful or biased content
   - Hallucinations observed
   - Error message
   - Other (requires explanation)
4. Add comments if needed
5. Click **Download Report**

### What Happens

A report file downloads to your device containing:
- The issue type and your comments
- The conversation context (your prompt and the agent's response)
- Agent configuration details
- Instructions for sending to support

**Note**: The report downloads locally - email it to the support address shown in the file.

## Best Practices

### Writing Effective Messages

1. **Be specific**: Clear, detailed questions get better answers
2. **Provide context**: Share relevant background information
3. **One topic at a time**: Focus on a single task per conversation
4. **Follow up**: Ask clarifying questions if needed

### Match Agent to Task

Choose agents based on what you need help with:
- Need code help? Look for technical agents
- Writing assistance? Try general or creative agents
- Domain questions? Find domain expert agents

### Examples

| Instead of... | Try... |
|--------------|--------|
| "Help me with this code" | "Can you help me debug this Python function that's returning None instead of the expected list?" |
| "Write a report" | "Help me write a quarterly sales report summarizing Q3 performance, focusing on enterprise growth" |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Enter | Send message |
| Shift + Enter | New line (don't send) |

## Troubleshooting

### Message Not Sending

1. Check your internet connection
2. Verify you're logged in
3. Try refreshing the page

### Slow Responses

- Complex questions may take more time
- Check the loading indicator
- Wait for the response to complete before sending follow-ups

### Agent Not Available

- The agent may be temporarily offline
- You may not have permission to access that agent
- Contact your Tenant Admin if you need access

### Unexpected Responses

If an agent responds unexpectedly:
- Verify you selected the right agent
- Check which datasets are attached
- Try rephrasing your question
