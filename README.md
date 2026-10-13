# QAEverest — Claude Code Plugin Marketplace

Official [Claude Code](https://code.claude.com/docs/en/plugins) plugin marketplace for **[QAEverest](https://qaeverest.ai)** — generate AI-powered test cases, build and run automation suites, and run security & performance checks without leaving your editor.

## Install

```
/plugin marketplace add abhilasha3-ai/qaeverest-claude-plugin
/plugin install qaeverest@qaeverest
```

Then set your API key in the environment before starting Claude Code:

```bash
export QAEVEREST_API_KEY=qae_your_key_here
```

Get a key free at <https://qaeverest.ai/api-client/signup> (no card needed). You can also connect from inside Claude Code with `/qaeverest:connect`.

## What's in this marketplace

| Plugin | Description |
|---|---|
| [`qaeverest`](claude-plugin/) | AI test generation (functional / API / UI / mobile), project-grounded test authoring, automation suites, execution reports, and security & performance checks. Ships 15 slash commands and 28 MCP tools. |

See the plugin's [README](claude-plugin/README.md) for commands, tools, and usage, and its [PRIVACY.md](claude-plugin/PRIVACY.md) for data handling.

## How it works

The plugin bundles its own MCP server — `claude-plugin/dist/server.cjs`, a single self-contained file — and Claude Code runs it directly with Node. There is no `npm install` and no `npx` download at startup.

That server is the same engine behind the QAEverest VS Code extension and JetBrains plugin, so the QA behaviour, the slash commands and the chat history format match what you get in those IDEs. Two things work differently here, because Claude Code has no modal dialogs or panel buttons:

- A flow that needs a value asks **through Claude**, which puts the question to you in chat and then continues.
- Anything that spends credits or starts a real run asks for **explicit approval** before it goes ahead.

Requires **Node.js 18+**.

## License

MIT — see [LICENSE](LICENSE).
