---
description: Generate QA test cases from a story, a file, or a feature description via QAEverest
argument-hint: [story text, a file path, or a feature description]
---

Generate QA test cases with QAEverest for: **$ARGUMENTS**

1. If `$ARGUMENTS` is empty, ask the user what to generate tests for and stop.
2. Call `qae_chat` with the request. If `$ARGUMENTS` names files in the repo, pass them in `files` rather than pasting their contents — QAEverest reads PDF, DOCX and XLSX as text, and a path keeps the story grounded in the real document.
3. Handle the reply:
   - `needs_input` — the generator needs mandatory fields (test type, domain, module). Ask the user, then call `qae_chat` again with `answers`.
   - `awaiting_approval` — generation costs credits. Show the user what is being proposed and what it costs, get a real yes or no, then call `qae_approve`.
4. Present the returned scenarios. Offer to save them to a `.feature`, `.csv` or `.xlsx` file — ask `qae_chat` to save, so they land in `qaeverest-tests/` the same way they do in the IDE extensions.

For tests grounded in this repo's actual code rather than a description, run `/qaeverest:inventory` first.
