# Managing Dataset Content

## Start Here

1. Open **Datasets** and select a dataset tile.
2. Review the documents table for status, errors, and duplicates.
3. Remove or replace stale files before major reviews.
4. Re-share or adjust group access when membership changes.

## Why this matters

Managing content keeps retrieval trustworthy—operators trust answers only when the underlying document set is current.

## Details

Dataset management in active Gen 3 stays inside the datasets workspace. Use the dataset documents view and the dataset edit form together to keep the retrieval set accurate, current, and appropriately shared.

## Typical management tasks

- review which documents are in the dataset
- remove outdated files
- upload replacement files
- confirm import results
- review sharing posture
- verify retrieval defaults such as embedding model and chunking strategy

## Document-level review

Open the dataset documents view when you need to inspect the files inside one dataset. This is the right place to confirm whether ingestion succeeded and whether old material should be removed.

## Dataset-level review

Return to the dataset edit workflow when you need to change:

- name or description
- access posture
- group sharing
- retrieval defaults
- other metadata that affects how the dataset should be used

## Management workflow

1. Open the dataset.
2. Review the current document list.
3. Remove outdated or incorrect material.
4. Upload or import replacement content.
5. Re-check the sharing posture.
6. Validate the result in [GT Chat](gen3/chat) or in any agent that depends on the dataset.

## When to edit the dataset instead of the agent

If the problem is bad or missing source material, fix the dataset. If the problem is how the agent uses otherwise-correct source material, then review the agent instead. Separating those two causes prevents unnecessary agent churn.

## Best practices

- Keep one dataset aligned to one coherent body of source material.
- Remove stale files promptly so retrieval does not mix old and new guidance.
- Revisit group sharing after imports, because imported content may deserve a narrower or broader audience.
- Test the real downstream workflow after major changes.

## Related pages

- [Datasets](gen3/datasets)
- [Uploading and Importing Documents](gen3/datasets/uploading)
- [Agents](gen3/agents)
