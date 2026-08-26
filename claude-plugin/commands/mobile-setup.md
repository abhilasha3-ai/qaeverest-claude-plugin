---
description: Configure QAEverest mobile automation — device farm, app binary, and handset
---

Call `qae_mobile_setup`.

The setup form is an interactive page, and Claude Code has no surface for one — so this returns a link to it in the QAEverest web app, plus whichever device profiles are already configured. Give the user the link and summarise what is and isn't set up.

Never ask the user for device-farm credentials here, and never put them in a tool call. They belong in the web app, which is why this command sends them there.

Once they've set it up, a mobile suite can be started with `/qaeverest:run-suite`.
