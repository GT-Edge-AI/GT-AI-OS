# Datasets

## Start Here

1. Open **Datasets** from the tenant sidebar.
2. Create a dataset for each logical corpus (project, unit, assessment cycle).
3. Upload or import documents ([Uploading and Importing Documents](gen3/datasets/uploading)).
4. Attach datasets in chat or agent defaults when you are ready to query them.

## Why this matters

Datasets are the durable knowledge layer for chat retrieval, workflow review, and GT API upload automation.

## Details

Datasets are the active Gen 3 retrieval boundary for tenant documents. The current `Datasets` page owns dataset creation, document upload/import, ZIP import/export, document review, sharing posture, and deletion. Gen 3 no longer relies on a separate tenant `Documents` route for normal document operations.

## What you do on the Datasets page

- create new datasets
- edit dataset metadata and retrieval defaults
- upload files directly into a dataset
- import datasets from ZIP bundles or legacy document bundles
- export one or more datasets
- open the per-dataset document view
- share datasets privately, to groups, or more broadly when allowed by the deployment

## How the page is organized

### Dataset list and filters

The page includes GT2-style search and filter controls so you can narrow the list by ownership, category, tags, access posture, and sort order before opening a specific dataset.

### Bulk actions

Datasets supports bulk export, bulk delete, and bulk upload entry points so you do not have to open one dataset at a time for every operation.

### Per-dataset document workspace

Opening a dataset's document modal lets you inspect the current document list, upload more files, import additional documents, and remove outdated content.

## Common tasks

### Create a dataset

1. Open `Datasets`.
2. Select **Create Dataset**.
3. Enter the dataset name and optional description.
4. Choose the access posture and any required group shares.
5. Save the dataset.

### Add source material

Use direct upload when you already know the destination dataset. Use import when you are bringing in a packaged dataset archive or a larger prepared file set.

### Review dataset content

Open the dataset's documents view to confirm the files present, the ingestion results, and whether outdated material should be removed or replaced.

## Datasets and chat

Datasets can be used in two places:

- as default datasets attached to an [agent](gen3/agents)
- as conversation-level datasets attached inside [GT Chat](gen3/chat/using-datasets)

Use agent defaults for repeatable workflows and conversation-level attachments for one-off context.

## Sharing model

Dataset visibility depends on the access option selected for the dataset and, when group-shared, on the relevant [group](gen3/groups). If another user cannot see a dataset, check its sharing posture before assuming the upload failed.

## Best practices

- Use clear dataset names that match a team, project, or content purpose.
- Remove outdated documents instead of leaving conflicting versions in the same retrieval set.
- Prefer group sharing over broad visibility when the content is team-specific.
- Revisit retrieval defaults after import so the dataset uses the intended embedding and chunking posture.

## Supporting pages

- [Uploading and Importing Documents](gen3/datasets/uploading)
- [Managing Dataset Content](gen3/datasets/managing)
- [Using Datasets in Chat](gen3/chat/using-datasets)
- [Groups](gen3/groups)
