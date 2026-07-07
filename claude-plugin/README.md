# QAEverest — Claude Code Plugin

Generate AI-powered test cases — and run security & performance checks — from inside Claude Code. This plugin bundles the [QAEverest MCP server](https://www.npmjs.com/package/qaeverest-mcp) plus ready-made slash commands.

## What you get

**Slash commands**

| Command | What it does |
|---|---|
| `/qaeverest:generate-tests <story\|file\|description>` | Generate functional / API / UI / mobile test cases from a story, a file, or a description |
| `/qaeverest:security-scan <url>` | Run a security scan (headers, SSL/TLS, common vulnerabilities) against a URL |
| `/qaeverest:usage` | Show credits remaining, monthly requests, and enabled services |

**MCP tools** (the agent picks these automatically when you describe what you want)

`generate_testcases` · `generate_api_tests` · `generate_ui_tests` · `generate_mobile_tests` · `security_scan` · `performance_test` · `get_usage`

## Prerequisites

- **Node.js 18+** (the plugin runs the server via `npx`)
- A **QAEverest API key** (`qae_...`) — [sign up free](https://app.qaeverest.ai/api-client/signup?source=claude-plugin) (100 credits, no card) or get one from **Admin → API Management**.

## Setup

1. Install the plugin from the directory (or add this repo as a plugin marketplace).
2. Make your API key available to Claude Code as an environment variable:

   ```bash
   export QAEVEREST_API_KEY=qae_your_key_here
   ```

   The bundled [`.mcp.json`](.mcp.json) reads `${QAEVEREST_API_KEY}` from the environment — your key is never stored in the plugin.
3. Restart Claude Code. Try: `/qaeverest:usage`.

## Example prompts

> *"Generate functional test cases for the login story in `auth/README.md` and save them as a feature file."*
>
> *"Generate API tests from this `openapi.yaml`, then scaffold Playwright specs from them."*
>
> *"Run a full security scan against https://staging.example.com."*

## Billing & scope

Each generation/scan/performance call is billed to your QAEverest account at an admin-configured per-service credit cost. Whether a given tool works depends on which services are **enabled** for your API key — check with `/qaeverest:usage`. Only scan or load-test hosts you are authorized to test.

## Privacy

See [PRIVACY.md](PRIVACY.md) for what data the server sends to the QAEverest backend and how it's handled.

## License

MIT — see [LICENSE](LICENSE).
