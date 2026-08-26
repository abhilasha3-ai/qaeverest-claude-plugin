---
description: Ask the QAEverest QA copilot anything — the same assistant as the VS Code and JetBrains panels
argument-hint: [what you want to test, build, run, or ask about]
---

Send this to the QAEverest copilot: **$ARGUMENTS**

Call `qae_chat` with the message verbatim. Do not rephrase it into a "better" prompt — the copilot does its own intent detection, and reworded requests are how the wrong engine gets picked.

Then:
- `needs_input` → ask the user those exact questions, call again with `answers`.
- `awaiting_approval` → relay the proposed action and its cost, wait for the user's answer, then `qae_approve`. Never approve on the user's behalf.
- Otherwise, relay the reply as-is. It is already Markdown.

If `$ARGUMENTS` is empty, ask what they'd like to do and mention the shortcuts: `/qaeverest:generate-tests`, `/qaeverest:scan-project`, `/qaeverest:inventory`, `/qaeverest:run-suite`, `/qaeverest:report`.
