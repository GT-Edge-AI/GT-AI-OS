# Using Datasets in Conversations

You can give agents access to your documents during a conversation using the dataset selector. This allows agents to search your content and provide informed responses.

## How It Works

When you add datasets to a conversation:
1. The agent can search those datasets for relevant information
2. Context from your documents is included with your messages
3. The agent uses this information to provide better answers

## Two Ways to Add Datasets

### Agent-Configured Datasets

Datasets can be permanently attached to an agent in the agent's configuration settings. These datasets are automatically available in every conversation with that agent.

This is useful for:
- Standard reference materials an agent should always access
- Company documentation or policies
- Domain-specific knowledge bases

### Conversation Datasets

You can also add datasets to a specific conversation for temporary access:

1. Click the **Paperclip icon** (to the left of the message input)
2. A popover opens titled "Add Datasets to Conversation"
3. Upload new files or select existing datasets
4. The agent can now search these datasets during this conversation

## Adding Datasets to a Conversation

### Option 1: Upload New Files

Upload files directly to create a new dataset:

1. In the popover, use the **Upload files** area
2. **Drag and drop** files or **click** to browse
3. A dataset is automatically created (named with a timestamp)
4. Wait for processing to complete
5. The dataset is automatically selected for the conversation

Auto-created datasets are marked with an amber **"auto"** badge so you can identify them later.

**Important:** Files are processed (text extracted, chunked, and embedded) before they become available. This may take a few moments depending on file size.

### Option 2: Select Existing Datasets

Use datasets you've already created:

1. In the popover, browse the list of your available datasets
2. Check the box next to each dataset you want to include
3. Selected datasets are immediately available to the agent

### Removing Datasets

To remove a dataset from the conversation:
1. Open the dataset selector (click the Paperclip icon)
2. Uncheck the dataset you want to remove
3. The agent will no longer reference that dataset

## Supported File Types

When uploading files, the following formats are supported:

| Type | Extensions |
|------|------------|
| Documents | PDF, DOCX, TXT, MD |
| Data | CSV, JSON |

**Maximum file size:** 50MB per file

**Not supported:** Images, videos, audio files, RTF, XML, HTML, Excel (.xlsx)

**Tip:** Convert Excel files to CSV before uploading for best results.

## Tips for Better Results

### Be Specific
Tell the agent what you want from your documents:
- "Summarize the key findings from the attached report"
- "What does the policy say about vacation time?"
- "Find all mentions of [topic] in these documents"

### Use Focused Datasets
Smaller, focused datasets often work better than large ones. If you have a lot of documents, organize them into separate datasets by topic.

### Check Processing Status
Files need to be fully processed before the agent can search them. If you just uploaded a file and don't get relevant results, wait a moment and try again.

### Combine with Agent Knowledge
Datasets work best when combined with an agent's built-in capabilities. Use datasets for your specific content, and let the agent provide general knowledge.

## Troubleshooting

### Agent Not Finding Information

If the agent isn't finding content from your datasets:
1. Verify the dataset is selected (check mark visible)
2. Confirm the document was fully processed
3. Try more specific queries
4. Check that the content exists in text form (images within PDFs aren't searchable)

### Upload Failing

If file uploads fail:
1. Check the file is under 50MB
2. Verify it's a supported file type (PDF, DOCX, TXT, MD, CSV, JSON)
3. Try a different file format
4. Refresh the page and try again

### Slow Processing

Large files take longer to process. You can continue the conversation while files process - they'll become available once complete.
