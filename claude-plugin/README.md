# QAEverest — Claude Code Plugin

The QAEverest QA copilot, in Claude Code.

This is the **third host** for `extension-core`, after the VS Code extension (which runs it in-process) and the JetBrains plugin (which runs it in a Node sidecar). Same engine, same commands, same chat history format — so a fix in the core lands in all three, and a QA workflow you know from the IDE works here unchanged.

## What you get

### Slash commands — the VS Code command palette, one for one

| Command | What it does |
|---|---|
| `/qaeverest:chat <anything>` | Ask the QA copilot — the chat panel, as a command |
| `/qaeverest:generate-tests <story\|file\|description>` | Generate functional / API / UI / mobile test cases |
| `/qaeverest:scan-project` | Build a Repo Map — stack, entry points, files worth testing (local, free) |
| `/qaeverest:index-project [full]` | Index the codebase so generation can cite real code |
| `/qaeverest:search-project <question>` | Semantic search over the indexed codebase |
| `/qaeverest:inventory` | Ranked inventory of testable features, then generate from the ones you pick |
| `/qaeverest:run-suite <suite> <url>` | Execute an automation suite |
| `/qaeverest:report` | Save the HTML execution report for the last run |
| `/qaeverest:mobile-setup` | Device farm, app binary and handset configuration |
| `/qaeverest:security-scan <url>` | Headers, SSL/TLS and common vulnerability checks |
| `/qaeverest:performance-test <url>` | Load / stress / spike / soak test |
| `/qaeverest:connect [key]` | Connect an account, or check the connection |
| `/qaeverest:usage` | Credits, key type, backend, configuration warnings |
| `/qaeverest:new-chat` | Start a fresh conversation |

### MCP tools

Claude picks these itself when you describe what you want, so you rarely need to name one:

`qae_chat` · `qae_approve` · `qae_status` · `qae_connect` · `qae_disconnect` · `qae_scan_project` · `qae_index_project` · `qae_search_project` · `qae_build_inventory` · `qae_select_features` · `qae_generate_from_features` · `qae_list_suites` · `qae_run_suite` · `qae_save_report` · `qae_open_report` · `qae_security_scan` · `qae_performance_test` · `qae_mobile_setup` · `qae_new_chat` · `qae_history` · `qae_open_chat`

## Setup

1. Install the plugin from this repo's marketplace.
2. Give Claude Code your QAEverest API key:

   ```bash
   export QAEVEREST_API_KEY=qae_your_key_here
   ```

   Or run `/qaeverest:connect` and paste it once — it is stored in `~/.qaeverest/credentials.json` with mode `0600`, and never in the plugin.
3. `/qaeverest:usage` to check it works.

No API key yet? [Sign up free](https://app.qaeverest.ai/api-client/signup?source=claude-plugin) — 100 credits, no card — or get one from **Admin → API Management**.

**Requires Node 18+.** The server ships as a single bundled file (`dist/server.cjs`); there is nothing to `npm install`.

## How it differs from the IDE extensions

Two things an editor can do that a Claude Code tool call cannot, and what happens instead:

**Dialogs.** When a flow needs a value it doesn't have — a search query, a test type, a domain — the IDE opens an input box. Here the tool returns `needs_input` with the questions, Claude asks you in chat, and calls the tool again with your answers. The core's slot-filling logic is untouched; only who does the asking changes.

**Approvals.** When the copilot proposes something that costs credits or starts a real run, the IDE shows an approve/reject card. Here the tool returns `awaiting_approval`, Claude asks you, and `qae_approve` settles it. **Nothing bills without that round trip** — and Claude is instructed not to answer on your behalf.

One thing genuinely isn't available: the **mobile setup form** is an interactive page, and there is no surface for one here. `/qaeverest:mobile-setup` links you to the same form in the QAEverest web app, which is what the core already does for a host without HTML panels.

## Where things are written

| Path | What |
|---|---|
| `.qaeverest/chats/` | Conversation history, per project (git-ignored) |
| `.qaeverest/state.json` | Repo map, file hashes, feature inventory |
| `.qaeverest/panels/` | Rendered HTML panels |
| `qaeverest-tests/` | Generated test-case files |
| `qaeverest-reports/` | HTML execution reports |
| `~/.qaeverest/credentials.json` | Your API key, mode `0600` |
| `~/.qaeverest/settings.json` | Per-user settings |

Settings can also come from the environment: `qaeverest.apiUrl` is `QAEVEREST_API_URL`, `qaeverest.openLinks` is `QAEVEREST_OPEN_LINKS`, and so on. Environment wins, then `.qaeverest/settings.json` in the project, then the one in your home directory.



## Billing & scope

Generation, suite runs, scans and performance tests are billed to your QAEverest account at an admin-configured per-service credit cost. Which tools work depends on which services are **enabled** for your key — check with `/qaeverest:usage`. Only scan or load-test hosts you are authorized to test.

## Related

- [`qaeverest-mcp`](https://www.npmjs.com/package/qaeverest-mcp) — the standalone MCP server for Cursor and other MCP clients. It talks to the public QAEverest API directly and does not carry the project-grounding, suite or report features this plugin gets from `extension-core`.

## Privacy

See [PRIVACY.md](PRIVACY.md) for what is sent to the QAEverest backend and how it is handled.

## License

MIT — see [LICENSE](LICENSE).
