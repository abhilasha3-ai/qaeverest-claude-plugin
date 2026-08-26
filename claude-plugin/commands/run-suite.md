---
description: Run a QAEverest automation suite against an environment
argument-hint: [suite name or id] [base URL]
---

Run a suite: **$ARGUMENTS**

1. Call `qae_list_suites` and match `$ARGUMENTS` against the results. If nothing matches, or several do, show the list and ask which one.
2. A run needs a target environment. If the user hasn't named a base URL, ASK — do not infer one from the repo, a config file, or an earlier conversation. Starting a real run against the wrong environment is the failure this step exists to prevent. Mobile suites are the exception: they run on a device, so no URL applies.
3. Confirm with the user that they want to start a real run against that target, then call `qae_run_suite`.
4. If the reply asks for mobile device or app setup, relay it and point them at `/qaeverest:mobile-setup`.
5. When the run finishes, offer `/qaeverest:report`.

Only run against hosts the user is authorized to test.
