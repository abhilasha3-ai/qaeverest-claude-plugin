---
description: Run a saved AI agent suite and report its release-gate verdict
argument-hint: "[suite name or id] [endpoint, optional]"
---

Run an AI agent suite: **$ARGUMENTS**

1. Call `qae_agent_suites` and match `$ARGUMENTS` against the results. If nothing matches, or several do, show the list and ask which one. No suites means none has been saved yet: they're saved from a run in the web app's AI Agent Testing.
2. The run goes to the suite's saved agent unless the user named another endpoint (e.g. staging). Use only an endpoint the user typed; never infer one from the repo or a config file. If the agent needs its own API key and the user hasn't given one, ask.
3. Confirm with the user that they want to start a real, billed run that sends conversations to that agent, then call `qae_agent_run`.
4. A run takes minutes. Call `qae_agent_run_status` with the run id to follow it; while the verdict is `pending`, say so and check again later instead of polling in a tight loop. Pass `min_trust_score`, `max_breaches` or `fail_on_no_baseline` only if the user asked for those thresholds.
5. Report the verdict (pass, fail or error), the trust score and every reason. If there was no comparable baseline, say that the gate couldn't compare and that pinning a baseline from a good run fixes it.

Only run against agents the user is authorized to test. Consumes credits.
