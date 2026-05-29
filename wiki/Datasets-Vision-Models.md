# Vision Models

Vision models add AI-powered image understanding to your datasets. When a vision model is selected on a dataset, uploaded images are automatically analyzed to generate searchable descriptions — making your image content accessible through conversations with agents.

## What Vision Models Do

When you upload images to a dataset with a vision model configured:

1. **Image analysis** — The vision model examines each image and generates a detailed text description covering objects, text, layout, and visual elements. Images embedded in PDFs are automatically extracted and analyzed individually as well.
2. **Embedding** — The description is indexed as searchable content in your dataset
3. **RAG search** — Agents can find and reference your images when answering questions
4. **On-demand deep analysis** — During a conversation, agents will refer to the source image for a closer, more targeted look based on your prompt.

Without a vision model selected, uploaded images are stored with basic metadata only (filename, dimensions, file size) and will not be searchable by content.

## Preparing A Dataset Connected to a Vision Model

### To Create the New Vision Enabled Dataset

1. Go to **Datasets** in the sidebar
2. Click **Create Dataset**
3. Fill in the name, description, and category
4. In the **Vision Model** dropdown, select a model (Llama 4 Maverick is selected by default)
5. Click **Create Dataset**
6. Click **Upload Documents** button and select the images you want to upload

### To Add Vision Capability to an Existing Dataset

1. Open the dataset details page
2. Click **Edit**
3. Find the **Vision Model** dropdown (marked with a purple eye icon)
4. Select a vision model from the list
5. Click **Update Dataset**
6. Delete pre existing files that require image processing

> **Important:** Changing the vision model affects future uploads only. Images already in the dataset keep their existing descriptions. To re-analyze existing images with a new vision model, re-upload them.

## Supported Image Formats

| Format | Extension | Notes |
|--------|-----------|-------|
| PNG | .png | Best for screenshots, diagrams, text-heavy images |
| JPEG | .jpg, .jpeg | Best for photographs |
| WebP | .webp | Modern format, good compression |

Images are supported alongside your usual text document file formats (PDF, Word, text, etc.). When you upload a PDF that contains embedded images, those images are automatically extracted and analyzed by the vision model — so your visual content is searchable even when it's inside a document.

## Uploading Images

### From the Datasets Page

1. Open your dataset (must have a vision model selected)
2. Click **Upload Documents** or drag files into the upload area
3. Select your image files — PNG, JPG, and WebP are all supported
4. Wait for processing to complete — the vision model will analyze each image
5. Images appear in the dataset details alongside your other documents

### From a Conversation

1. In any conversation, click the **paperclip icon** to open the dataset panel
2. At the top of the panel, you'll see a drag-and-drop area — drop your images there (or click to browse)
3. Choose whether to upload into an existing dataset or create a new one
4. Click **Upload** — the files start processing and the dataset is automatically attached to your conversation

**Note:** You can rename a dataset that is created during the file upload process in the Datasets menu.

## Chatting with Image Context

Once images are uploaded to a vision-enabled dataset:

1. Start or continue a conversation with any agent that is attached to the vision-enabled dataset
2. For example: click the **paperclip icon** and check the box next to a dataset that contains images
3. Send your message — the agent will now reference both your documents and image files that are included in your vision enabled dataset

> **Important:** Your dataset must have a Vision Model selected for images to be analyzed. Without a vision model configured, uploaded images won't be processed for content.

## What to Expect

### Vision models are good at

| Capability | Example |
|-----------|---------|
| Describing scenes and objects | "A bar chart showing Q3 revenue by region" |
| Identifying text in images | Reading labels, signs, document text |
| Recognizing visual elements | Logos, icons, UI components, charts, diagrams |
| Categorizing content | Photos vs. screenshots vs. diagrams |
| Summarizing visual information | Key takeaways from infographics or dashboards |

### Vision models have limitations

| Limitation | Details |
|-----------|---------|
| Not pixel-perfect | May miss fine details, small text, or low-contrast elements |
| Interpretation varies by model | Different vision models may describe the same image differently |
| Quality depends on input | Clear, well-lit, high-resolution images with clearly defined borders or image outlines produce better results |
| Not a replacement for human review | Always verify critical details — treat AI descriptions as a helpful starting point |

## Available Vision Models

The vision models available on your instance depend on what your **Super Admin** has provisioned. Other options may include models from various providers — check with your Tenant Admin to request additional models.

**Tip:** Different models may produce different quality results for different types of images. Try multiple models to see which works best for your use case.

## Pro Tips

| Tip | Why |
|-----|-----|
| **Start with a small test dataset** | Upload a few sample images to evaluate vision model results before committing to large batches |
| **Try different vision models** | Switch models on your dataset (Edit → Vision Model dropdown) and re-upload to compare description quality |
| **Use high-quality images** | Clear, well-lit, high-resolution images produce significantly better descriptions |
| **Experiment with file types** | PNG for screenshots and text-heavy images, JPEG for photos, WebP for web content |
| **Search to check descriptions** | After uploading, ask an Agent to search your dataset to see what the vision model detected after initial upload |
| **Combine images with documents** | Mix connected images and text documents in a dataset for richer, multi-modal context |
| **Chat with a Vision Agent** | Upload files to a dataset and use an agent (such as the Vision Chat Agent template below) that's optimized for image Q&A |

## Vision Chat Agent Template

Get started quickly with a pre-configured agent optimized for chatting with datasets that contain images.

This agent is designed to help you analyze, discuss, and ask questions about images in your datasets.

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Vision Chat Agent Template](https://github.com/GT-Edge-AI-Internal/GT-AI-OS-Instructions/blob/main/agent-templates/vision-chat-agent.csv)**

### How to Use

1. Download the Agent Template CSV file using the link above
2. Go to **Agents** in the sidebar
3. Click **Import** in the top right
4. Select the downloaded CSV file
5. Review the agent configuration
6. Click **Import** to create the agent
7. The agent will appear on the Agent Configuration list and can be added to your Favorites list by clicking on the **Add Favorites** button
8. Start a new conversation with the Vision Chat Agent
9. Click the **paperclip icon** and select a dataset that contains images
10. Ask questions about your images per the examples listed below

### Example Questions

a. "What do the images in this dataset show?"

b. "Is there any text visible in these images?"

c. "Describe the diagram in the uploaded screenshot"

d. "Compare the images and summarize key differences"

See [Agent Templates](agents/templates) for more details on importing and customizing templates.

## Troubleshooting

### Images Not Being Analyzed

1. **Check vision model selection:** Open the dataset → click Edit → verify a vision model is selected in the dropdown
2. **Verify image format:** Only PNG, JPG, and WebP are supported
3. **Ensure image upload processing is complete:** Image analysis can commence after upload and processing is fully completed

### Vision Agent is Providing Poor Quality Responses to Questions

1. Use more specific instructions in your user prompts when requesting the Agent analyze your desired images — such as saying what specifically you want it to find in the images, or for what purpose you want the images to be analyzed
2. Use higher resolution images with good lighting and contrast
3. Try a different vision model (edit dataset → change model → re-upload images)
4. Simple, focused images with clear subjects produce better results than busy or cluttered images

### Agent Not Finding Image Content

1. Verify the dataset is attached to the conversation (click the paperclip icon)
2. Confirm images have been processed (check the document list in dataset details)
3. Try more specific search queries related to what the vision model would describe
4. Remember: without a vision model selected, images have only basic file metadata

## Next Steps

1. [Creating Datasets](datasets/creating) — Full guide to dataset setup
2. [Managing Documents](datasets/managing-documents) — Add and organize files in datasets
3. [Using Datasets in Chat](chat-interface/using-datasets) — Attach datasets to conversations
4. [Agent Templates](agents/templates) — Browse all available agent templates
