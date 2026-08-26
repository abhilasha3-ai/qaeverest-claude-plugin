---
description: Build (or re-show) the ranked inventory of testable features in this project
---

1. Call `qae_select_features` first — it re-displays an inventory already built in this session and costs nothing.
2. If it says it is showing a SAMPLE, call `qae_build_inventory` to analyse the real project. Tell the user this takes a few minutes on a large repo.
3. Present the recommended features and their ids.
4. Ask which ones they want tests for, then call `qae_generate_from_features` with those ids. Each feature's cited source files are read and sent as grounding, so the cases describe what the code actually does.

Generation consumes credits — if the reply is `awaiting_approval`, get the user's decision before calling `qae_approve`.
