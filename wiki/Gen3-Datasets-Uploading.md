# Uploading and Importing Documents

## Start Here

1. Open **Datasets** and select or create a target dataset.
2. Use upload, import, or URL ingestion controls supported by your tenant.
3. Wait until documents show ready/processed status.
4. Attach the dataset in **GT Chat** or reference it from agent configuration.

## Why this matters

Clean ingestion upfront prevents chat blocking and wrong answers caused by half-processed files.

## Details

Uploading in Gen 3 is dataset-first. Normal document work happens inside [Datasets](gen3/datasets) or, for one-off conversational context, from [GT Chat](gen3/chat/using-datasets). The retired tenant `Documents` page is not part of the active workflow.

## Upload paths in the current product

### Upload into an existing dataset

Use this when you already know the correct dataset and want the files to become part of that reusable retrieval set.

### Bulk upload

Use the bulk upload shelf when you want to stage several files into one dataset without opening each dataset individually.

### Import a dataset archive

Use the dataset import workflow when you have a ZIP export or legacy dataset bundle that should recreate a dataset rather than just add a few new files.

### Upload from chat

Use chat uploads only when the files are primarily for the current conversation or you want to stage quick working material before deciding how to organize it permanently.

## Recommended sequence

1. Choose or create the correct dataset.
2. Upload or import the files.
3. Wait for ingestion and processing to complete.
4. Open the dataset documents view to verify the results.
5. Re-test the affected workflow in [GT Chat](gen3/chat) if the files were meant to improve agent answers.

## Import considerations

Gen 3 can validate an import bundle before completing the import. Review the validation output carefully, especially when the bundle includes retrieval defaults or sharing posture that may not match the destination tenant.

If the import prompts for re-embedding or compatibility review, make that decision before assuming the imported dataset is ready for production use.

## Best practices

- Create the right dataset first instead of uploading into a temporary location and reorganizing later.
- Use meaningful dataset names so imported or uploaded content stays discoverable.
- Prefer the datasets page for reusable content and chat upload only for temporary conversational context.
- Confirm processing is complete before judging answer quality in chat.

## Related pages

- [Datasets](gen3/datasets)
- [Managing Dataset Content](gen3/datasets/managing)
- [Using Datasets in Chat](gen3/chat/using-datasets)
