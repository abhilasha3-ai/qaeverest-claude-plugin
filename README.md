# QAEverest — Claude Code Plugin Marketplace

Official [Claude Code](https://code.claude.com/docs/en/plugins) plugin marketplace for **[QAEverest](https://qaeverest.ai)** — generate AI-powered test cases and run security & performance checks without leaving your editor.

## Install

```
/plugin marketplace add abhilasha3-ai/qaeverest-claude-plugin
/plugin install qaeverest@qaeverest
```

Then set your API key in the environment before starting Claude Code:

```bash
export QAEVEREST_API_KEY=qae_your_key_here
```

Get a key free at <https://app.qaeverest.ai/api-client/signup> (100 credits, no card).

## What's in this marketplace

| Plugin | Description |
|---|---|
| [`qaeverest`](claude-plugin/) | AI test generation (functional / API / UI / mobile) + security & performance checks via the QAEverest public API. Ships 3 slash commands and 7 MCP tools. |

See the plugin's [README](claude-plugin/README.md) for commands, tools, and usage, and its [PRIVACY.md](claude-plugin/PRIVACY.md) for data handling.

## How it works

The plugin runs the [`qaeverest-mcp`](https://www.npmjs.com/package/qaeverest-mcp) server (from the public npm registry) via `npx` and talks to the QAEverest API. No QAEverest source code is required or included here.

## License

MIT — see [LICENSE](LICENSE).
