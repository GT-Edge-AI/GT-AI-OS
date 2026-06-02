# Self-Hosted runbooks (browser only)

The `Gen3-Self-Hosted-*.md` pages are **host operator runbooks** for README and GitHub wiki browsing.

**Do not** add them to:

- `_gt3-index.json` (tenant **GT AI OS Instructions** nav)
- `_gt3-super-admin-index.json` (Control Panel **Instructions** / **GT Helper** super-admin corpus)

The cluster only loads articles whose slugs appear in those index files (`SlugAllowedInTree` / `SlugAllowedInTenantWiki`). Prewarm and Helper RAG walk the index tree only.

`_Sidebar.md` affects **GitHub wiki** sidebar navigation when published; it does **not** drive in-app Instructions.

When publishing via `gt-ai-os/scripts/publish-public-instructions-content.sh`, these files sync to the product repo `wiki/` folder like other markdown, but remain excluded from in-app nav unless an operator deliberately edits the JSON indexes (not part of this documentation set).
