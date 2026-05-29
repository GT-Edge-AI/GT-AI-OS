# Documents in Gen 3

## Start Here

1. Do not expect a standalone **Documents** route in Gen 3.
2. Use [Datasets](gen3/datasets) for reusable document libraries.
3. Use [GT Chat](gen3/chat) paperclip uploads for conversation-scoped files.

## Why this matters

Gen 3 consolidated document work into datasets and chat to avoid duplicate hubs that diverged from retrieval behavior.

## Details

The standalone tenant `Documents` page is no longer part of the active Gen 3 route surface.

## Where document work happens now

Document workflows now stay inside:

- [Datasets](gen3/datasets) for reusable dataset-backed document management
- [Uploading and Importing Documents](gen3/datasets/uploading) for dataset-first ingestion flows
- [Managing Dataset Content](gen3/datasets/managing) for per-dataset document review, cleanup, and updates
- [Using Datasets in Chat](gen3/chat/using-datasets) for one-off conversational uploads and attached dataset context

## Practical guidance

If your goal is to curate a reusable source collection, start in [Datasets](gen3/datasets).

If your goal is to add temporary working files to a conversation, use the chat dataset/upload controls in [GT Chat](gen3/chat).

This page remains only as migration context for older Gen 3 references and should not be treated as an active navigation destination.
