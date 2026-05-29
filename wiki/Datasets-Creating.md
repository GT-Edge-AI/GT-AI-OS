# Creating Datasets

This guide walks you through creating and setting up datasets in GT AI OS step by step.

## Prerequisites

- You need appropriate permissions to create datasets
- Have documents ready to upload

## Creating a New Dataset

### Step 1: Access Dataset Creation

1. Go to **Datasets** in the sidebar
2. Click **Create Dataset**
3. The creation form opens

### Step 2: Basic Information

Fill in the dataset details:

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| **Name** | Yes | Clear, descriptive name | "Q3 2024 Sales Reports" |
| **Description** | Yes | What this dataset contains | "Quarterly sales data and analysis for North America region" |
| **Category** | Yes | Category for organization | Create or select existing |
| **Tags** | No | Keywords for filtering | "sales", "q3", "2024", "reports" |

### Using Categories

Categories help organize datasets across your organization:

1. Select from existing categories or create a new one
2. Categories appear as filter options on the Datasets page
3. Common categories: Legal, Engineering, Sales, Marketing, HR, Operations

**Tip:** Coordinate with your team on category names to keep things consistent.

### Using Tags

Tags provide additional ways to find datasets:

1. Enter keywords relevant to the content
2. Press Enter or comma to add each tag
3. Tags are searchable and filterable
4. Use multiple tags to improve discoverability

**Tag examples:**
- Content type: "reports", "policies", "procedures", "templates"
- Time period: "q1-2024", "annual", "monthly"
- Department: "engineering", "sales", "legal"
- Status: "current", "archived", "draft"

### Step 3: Visibility Settings

Choose who can use this dataset:

| Visibility | Who Can Access | Best For |
|------------|----------------|----------|
| **Individual** | Only you | Personal knowledge bases |
| **Team** | Selected team members | Team-specific resources |
| **Organization** | All users in your organization | Company-wide knowledge |

**Note**: Only Tenant Admins can set Organization visibility. Once set, all users can access the dataset.

When selecting **Team** visibility:
1. Select which teams should have access
2. Team members will see the dataset in their list

### Step 4: Vision Model (Optional) *(Added in 2.0.36)*

Configure a vision model to enable AI-powered image analysis for documents in this dataset.

1. Find the **Vision Model** dropdown (marked with a purple eye icon)
2. A default vision model is pre-selected automatically
3. To disable image analysis, select **None - Images will not be analyzed**

| Option | Behavior |
|--------|----------|
| **Vision model selected** | Images in uploaded documents (PDFs, standalone images) are analyzed by AI. Descriptions are generated and made searchable via RAG. |
| **None** | Images are not analyzed. Standard text extraction only. |

**How it works:** When a vision model is configured, the system extracts images from your documents (including embedded images in PDFs), sends them to the vision model for analysis, and stores the generated descriptions as searchable chunks — making your visual content discoverable through natural language queries.

**Tip:** Leave the default vision model selected unless you have a specific reason to disable image analysis.

### Step 5: Create the Dataset

1. Review your settings
2. Click **Create Dataset**
3. The dataset is created (empty)
4. You're taken to the dataset detail view

## Adding Documents

### Step 6: Upload Your Documents

After creating the dataset:

1. Click **Upload Documents** or drag files into the upload area
2. Select files to upload

**Supported file types:**

| Type | Extension | Notes |
|------|-----------|-------|
| PDF | .pdf | Text is extracted automatically |
| Word | .docx | Modern Word format |
| Text | .txt | Plain text files |
| Markdown | .md | Markdown files |
| CSV | .csv | Tabular data |
| JSON | .json | Structured data |
| Image | .png, .jpg, .jpeg | Requires vision model for analysis |

**Limits:**
- Maximum 50MB per file

**Tip**: For Excel files (.xlsx), convert to CSV for best results.

### Step 7: Wait for Processing

When you upload documents:
1. **Uploading**: Files are transferred to the server
2. **Processing**: Text is extracted from files
3. **Chunking**: Text is split into searchable segments
4. **Embedding**: Each chunk is converted to a vector
5. **Image Analysis** (if vision model configured): Images are described by AI
6. **Complete**: Documents are ready for use

Processing time depends on document size and complexity. You can continue working while documents process.

### Step 8: Verify Upload

After processing completes:
1. Check that all documents appear in the list
2. Verify document counts and sizes
3. Note the chunk count (segments created)

## Using Your Dataset

### Attach to Agents

To give an agent permanent access to your dataset:
1. Edit the agent (or create a new one)
2. Scroll to the **Dataset Selection** section
3. Search for your dataset by name
4. Check the box next to your dataset
5. Save the agent

### Use During Chat

Add datasets to any conversation:
1. In the chat interface, click the paperclip icon
2. Select the dataset to reference
3. The agent can now search that dataset for the conversation

## Best Practices

### Naming Conventions

Use clear, descriptive names:
- Good: "Legal - Contract Templates 2024"
- Good: "Engineering - API Documentation"
- Avoid: "Documents" or "Stuff" or "New Dataset"

### Content Planning

Before creating:
- Identify what documents you'll include
- Consider who needs access
- Plan the category and tags
- Keep datasets focused on specific topics

### Quality Tips

| Tip | Why |
|-----|-----|
| Use focused datasets | Better retrieval than one large dataset |
| Keep documents updated | Remove outdated information |
| Include diverse content | Cover different aspects of a topic |
| Avoid duplicates | Same content in multiple documents hurts quality |

## Managing Your Dataset

### Adding More Documents

To add documents to an existing dataset:
1. Open the dataset
2. Click **Upload Documents**
3. Select new files
4. Wait for processing

### Removing Documents

To remove a document:
1. Open the dataset
2. Find the document in the list
3. Click the delete icon
4. Confirm removal

**Note**: Removing documents triggers re-indexing.

### Editing Dataset Info

To update name, description, category, or tags:
1. Open the dataset
2. Click **Edit**
3. Make your changes
4. Save

## Next Steps

After creating your dataset:
- [Add and manage documents](managing-documents)
- [Share with your team](sharing)
- Attach to agents to provide knowledge
