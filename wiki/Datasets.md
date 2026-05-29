# Datasets

Datasets are collections of documents that provide knowledge to AI agents. This guide helps you create, manage, and share datasets in GT AI OS.

## Quick Links

- [Creating Datasets](datasets/creating) - Upload documents and configure your dataset
- [Managing Documents](datasets/managing-documents) - Add, remove, and organize documents
- [Sharing Datasets](datasets/sharing) - Share with teams and export/import
- [Vision Models](datasets/vision-models) - Use AI vision to analyze and search images

## What is a Dataset?

A dataset is a collection of documents that can be:
- **Attached to agents** to give them specialized knowledge
- **Used in conversations** to provide context for your questions
- **Shared with team members** for collaborative work

When you attach a dataset to an agent or conversation, the agent can search your documents and use relevant information in its responses.

## How Datasets Work

1. **Upload documents** (PDF, Word, text files, images, etc.)
2. **Processing happens automatically** - text is extracted, split into chunks, and indexed
3. **Images are analyzed** (optional) - if a vision model is configured, images are described by AI and made searchable
4. **Attach to agents or conversations** - the agent can now search your content
5. **Ask questions** - relevant information is retrieved and used in responses

## Getting Started

### Creating Your First Dataset

1. Go to **Datasets** in the sidebar
2. Click **Create Dataset**
3. Enter a name and description
4. Upload your documents
5. Wait for processing to complete

See [Creating Datasets](datasets/creating) for a detailed guide.

### Using Datasets in Chat

You can add datasets to a conversation at any time:

1. Click the **Paperclip icon** in the chat interface
2. Select existing datasets or upload new files
3. The agent can now search your content

### Attaching Datasets to Agents

Give an agent permanent access to your documents:

1. Edit the agent
2. In the **Datasets** section, select datasets to attach
3. Save the agent

## Organizing Datasets

### Categories

Create categories to group related datasets (e.g., Legal, Engineering, Sales). Filter by category on the Datasets page.

### Tags

Add tags for additional filtering. Use consistent tags across your organization for easy discovery.

### Naming Conventions

Use clear, descriptive names:
- Good: "Q3 2024 Sales Reports"
- Good: "Engineering - API Documentation"
- Avoid: "Documents" or "New Dataset"

## Tips

- **Keep datasets focused** - smaller, topic-specific datasets often work better than large ones
- **Update regularly** - remove outdated documents and add new ones
- **Test retrieval** - ask questions to verify the agent finds relevant content
- **Share thoughtfully** - make datasets available to those who need them
