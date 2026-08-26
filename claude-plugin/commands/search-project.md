---
description: Semantic search over the indexed codebase — ask in plain English
argument-hint: [what to look for, e.g. how does login work]
---

Call `qae_search_project` with `query` set to **$ARGUMENTS**. If it's empty, ask the user what to look for.

Report the files and line ranges it found, with their scores. Offer to read the most relevant ones.

If nothing comes back, the project probably isn't indexed — suggest `/qaeverest:index-project`.
