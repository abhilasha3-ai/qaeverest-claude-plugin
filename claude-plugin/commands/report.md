---
description: Save and show the HTML execution report for the last QAEverest run
---

1. Call `qae_save_report`. It writes the report into `qaeverest-reports/` in this project, with per-test steps, durations and trend.
2. If there is no finished run to report on, say so and offer `/qaeverest:run-suite`.
3. Report the path it was written to, and summarise the outcome: how many passed, failed, and anything that stands out.

`qae_open_report` gives the path of the last report saved, if the user just wants to find it again.
