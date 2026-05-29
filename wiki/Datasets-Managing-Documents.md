# Managing Documents

This guide covers how to add, manage, and organize documents within datasets.

## Adding Documents

### Uploading Files

1. Open the dataset details page
2. Click **Upload Documents** or drag files to the upload area
3. Select files from your computer
4. Wait for processing to complete

### Supported File Types

| Type | Extensions | Notes |
|------|------------|-------|
| PDF | .pdf | Best for formatted documents |
| Word | .docx | Standard office documents |
| Text | .txt | Plain text files |
| Markdown | .md | Documentation, notes |
| CSV | .csv | Tabular data |
| JSON | .json | Structured data |

### Upload Limits

- Maximum file size: **50MB per file**
- Large files may take longer to process

## Document Processing

### What Happens During Processing

When you upload a document:

1. **Extraction**: Text is extracted from the file
2. **Chunking**: Text is split into searchable segments
3. **Embedding**: Each chunk is converted to a vector
4. **Indexing**: Vectors are stored for fast retrieval

### Processing Status

Documents show their status:
- **Pending**: Waiting to upload
- **Uploading**: File transfer in progress
- **Processing**: Being analyzed and embedded
- **Completed**: Available for use
- **Failed**: Error during processing

## Managing Documents

### Viewing Document Details

Click on a document to see:
- File name and type
- Upload date
- Processing status
- Chunk and vector counts

### Removing Documents

To delete a document:
1. Find it in the document list
2. Click the delete icon
3. Confirm removal

**Note**: Removal triggers reindexing of the dataset.

### Managing Multiple Documents

Documents are managed individually within a dataset. For bulk operations at the dataset level, use the Export and Import features on the Datasets page.

## Document Quality

### Best Practices for Source Documents

**Content quality:**
- Use clear, well-structured text
- Avoid scanned images (OCR limitations)
- Include context and definitions

**File quality:**
- Use native text formats when possible
- Ensure files aren't corrupted
- Keep file sizes reasonable

### Optimizing for Search

**Help agents find relevant content:**
- Use descriptive headings
- Include key terms naturally
- Organize content logically

## Troubleshooting

### Document Not Processing

If processing gets stuck:
1. Check file format is supported
2. Verify file isn't corrupted
3. Try uploading a smaller version
4. Contact support if issue persists

### Content Not Found in Searches

If expected content isn't retrieved:
1. Verify document processed successfully
2. Check content isn't in images (not searchable)
3. Try searching with exact phrases
4. Consider document chunking settings

### Poor Quality Results

If search results aren't relevant:
1. Review document content quality
2. Consider splitting large documents
3. Update chunking configuration
4. Add more context to documents
