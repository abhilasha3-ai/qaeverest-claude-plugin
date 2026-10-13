---
description: Connect a QAEverest account, or check the current connection
argument-hint: [qae_... API key, optional]
---

1. Call `qae_status` first. If it already reports a connection, show the key type and credits and stop — there is nothing to do.
2. If `$ARGUMENTS` looks like a `qae_` key, call `qae_connect` with it. It is validated and stored in `~/.qaeverest/credentials.json` with mode 0600.
3. Otherwise call `qae_connect` with no arguments to start browser sign-in, and give the user the URL and code it returns. They approve it in their browser; call `qae_connect` again afterwards to finish.

Never invent, guess, or complete a partial API key. If the user hasn't got one, point them at the free sign-up link the "Not connected" reply includes — no card needed.

`/qaeverest:usage` shows what the connected key can do. `qae_disconnect` forgets it.
