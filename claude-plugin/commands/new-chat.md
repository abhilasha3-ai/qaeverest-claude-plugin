---
description: Start a fresh QAEverest conversation
---

Call `qae_new_chat`.

Use this when switching to an unrelated feature: the copilot replays the transcript as context, so a stale conversation steers generation toward the wrong thing. Conversations are stored per project in `.qaeverest/chats/`.

`qae_history` lists earlier conversations and `qae_open_chat` reopens one, if the user wants to pick up where they left off instead.
