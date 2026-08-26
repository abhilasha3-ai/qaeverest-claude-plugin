---
description: Run a load, stress, spike or soak test against a URL
argument-hint: [https://target.example.com] [load|stress|spike|soak]
---

Run a performance test: **$ARGUMENTS**

1. If no URL is given, ask for one.
2. Confirm the user is authorized to load-test that host. This generates REAL traffic against the target — running it against something that isn't theirs, or against production without intending to, is the mistake to avoid here.
3. Call `qae_performance_test` with the URL, and pass the user's own wording in `message` — the mode, virtual users, duration and ramp-up are parsed out of it exactly as the IDE chat parses them.
4. Present latency percentiles, throughput and error rate, and say whether the result looks healthy for the load applied.

Consumes credits.
