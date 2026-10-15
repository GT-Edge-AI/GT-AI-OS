# Reviewing Files in Order

## Start Here

1. Put the files in a [dataset](gen3/datasets) and wait until processing finishes for the files you expect the agent to read. Pending and failed files can still be listed.
2. Open an agent that has that dataset attached, or attach the dataset in [GT Chat](gen3/chat) with the paperclip.
3. Ask the agent to list the files in the dataset.
4. Ask it to review the files you care about, in source order, and to continue until those files are covered.
5. If the reply stops mid-file, ask it to continue the review from where it left off.

## Why this matters

A dataset-backed agent can page through the file catalog and keep a source-ordered review going across files. You can see what is in the dataset, including files that are still pending or that failed processing, and a finished file does not end the review of the next relevant file.

## Details

This is how dataset-backed agents use dataset search during **GT Chat**. There is no separate review screen. The agent lists and reads files when the prompt asks it to catalog or review them. See [Document Review](gen3/workflows/document-review) for the chat setup, and [Managing Dataset Content](gen3/datasets/managing) for ingestion status.

### File catalog

When the agent lists files without a search phrase, it pages the catalog **40 files at a time**. The list includes pending and failed files, so you can see work that has not become searchable text yet.

Ask for the next page when the dataset is larger than one page.

### Ordered review

When you ask for a review in source order:

- The agent resumes after the last chunk it already returned, instead of reading the start of that file again.
- Finishing one file does not stop review of the next relevant file.
- A semantic search, where you ask a question and expect the closest passages, still returns at most **5** hits.

Name the files or the order you want when the dataset is large. A broad question still uses the 5-hit semantic search.

### When a file is missing from the answer

1. Open the dataset and check whether the file is pending, failed, or ready. See [Managing Dataset Content](gen3/datasets/managing).
2. Ask for a file list first so pending and failed names are visible.
3. Ask the agent to continue from the last file it finished.
4. Confirm the dataset is attached to this conversation or saved on the agent. See [Using Datasets in Chat](gen3/chat/using-datasets).

## Related pages

- [Datasets](gen3/datasets)
- [Document Review](gen3/workflows/document-review)
- [Using Datasets in Chat](gen3/chat/using-datasets)
- [Building Agents](gen3/agents/building)
