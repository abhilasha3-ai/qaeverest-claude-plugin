---
description: Show QAEverest credits remaining, key type, and which backend this project talks to
---

Call `qae_status` and report, concisely:
- Whether an account is connected, and the key type
- Credits remaining
- Whether this key can run suites, or is generation-only
- Any configuration warnings it returns

A configuration warning means this machine is pointed somewhere another machine isn't — usually a local backend URL left in settings. Explain what it means rather than just repeating it.

If credits are exhausted or a service is disabled, the fix is in the QAEverest portal (**Admin → API Management**), not here.
