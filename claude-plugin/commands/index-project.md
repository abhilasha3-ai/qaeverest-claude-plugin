---
description: Index this project into QAEverest so generated tests cite real code
argument-hint: [full]
---

Call `qae_index_project`. Pass `full: true` only if `$ARGUMENTS` contains "full", or the user says the index looks stale or empty — a full re-index re-sends every file.

Report how many files changed, how many chunks were stored, and whether the store confirmed them. If it reports 0 chunks stored, say so plainly and suggest a full re-index — that means the backend's store was reset, not that the project is empty.

Requires a connected account (`/qaeverest:connect`) and a reachable backend.
