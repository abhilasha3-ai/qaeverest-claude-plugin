# QAEverest — Claude Code Plugin

The QAEverest QA copilot, in Claude Code.

The plugin is the shared [QAEverest MCP server](https://www.npmjs.com/package/qaeverest-mcp), bundled, plus slash commands. It is the same server the VS Code, Cursor and JetBrains integrations give their agents, running the same engine as their panels (`extension-core`) — so a fix lands everywhere at once, and a QA workflow you know from the IDE works here unchanged.

## What you get

### Slash commands

<!-- qaeverest:commands -->
<!-- Generated from mcp-server/src/manifest.js by `npm run sync` in mcp-server/. -->

| Command | What it does |
|---|---|
| `/qaeverest:agent-test [suite name or id] [endpoint, optional]` | Run a saved AI agent suite and report its release-gate verdict |
| `/qaeverest:chat [what you want to test, build, run, or ask about]` | Ask the QAEverest QA copilot anything — generate tests, build and run suites, or ask about a run |
| `/qaeverest:connect [qae_... API key, optional]` | Connect a QAEverest account, or check the current connection |
| `/qaeverest:generate-tests [story text, a file path, or a feature description]` | Generate QA test cases from a story, a file, or a feature description via QAEverest |
| `/qaeverest:index-project [full]` | Index this project into QAEverest so generated tests cite real code |
| `/qaeverest:inventory` | Build (or re-show) the ranked inventory of testable features in this project |
| `/qaeverest:mobile-setup` | Configure QAEverest mobile automation — device farm, app binary, and handset |
| `/qaeverest:new-chat` | Start a fresh QAEverest conversation |
| `/qaeverest:performance-test [https://target.example.com] [load\|stress\|spike\|soak]` | Run a load, stress, spike or soak test against a URL |
| `/qaeverest:report` | Save and show the HTML execution report for the last QAEverest run |
| `/qaeverest:run-suite [suite name or id] [base URL]` | Run a QAEverest automation suite against an environment |
| `/qaeverest:scan-project` | Build a QAEverest Repo Map of this project — languages, frameworks, and the files worth testing |
| `/qaeverest:search-project [what to look for, e.g. how does login work]` | Semantic search over the indexed codebase — ask in plain English |
| `/qaeverest:security-scan [https://target.example.com]` | Run a QAEverest security scan against a URL |
| `/qaeverest:usage` | Show QAEverest credits remaining, key type, and which backend this project talks to |

<!-- /qaeverest:commands -->

### MCP tools

Claude picks these itself when you describe what you want, so you rarely need to name one:

<!-- qaeverest:tools surface=claude -->
<!-- Generated from mcp-server/src/manifest.js by `npm run sync` in mcp-server/. -->

| Area | Tool | What it does | Uses credits |
|---|---|---|---|
| Chat | `qae_chat` | Ask the QA copilot anything: generate tests, build or run a suite, ask about a run | yes |
|  | `qae_approve` | Settle an approval `qae_chat` asked for, with the user's own answer | yes |
|  | `qae_new_chat` | Start a fresh conversation | no |
|  | `qae_history` | List this project's conversations | no |
|  | `qae_open_chat` | Make an earlier conversation active again | no |
| Generate | `qae_generate_testcases` | Functional, system, SIT, database and other test cases from a story | yes |
|  | `qae_generate_api_tests` | API test cases from a description, an OpenAPI/Swagger spec or a Postman collection | yes |
|  | `qae_generate_ui_tests` | End-to-end UI automation test cases (navigate / click / type / assert) | yes |
|  | `qae_generate_mobile_tests` | Mobile automation test cases: gestures, device states, platform behaviour | yes |
| Your code | `qae_scan_project` | Repo Map: languages, frameworks, entry points, files worth testing (local) | no |
|  | `qae_index_project` | Index the codebase so generation can cite real code | no |
|  | `qae_search_project` | Semantic search over the indexed codebase | no |
|  | `qae_build_inventory` | Ranked inventory of testable features, with the files each came from | no |
|  | `qae_select_features` | Re-show the inventory with the ids to generate from | no |
|  | `qae_generate_from_features` | Test cases for inventory features, grounded in their source files | yes |
| Suites and runs | `qae_list_suites` | Automation suites on the account, with their ids | no |
|  | `qae_run_suite` | Execute an automation suite against an environment | yes |
|  | `qae_save_report` | Write the HTML report for the last run into `qaeverest-reports/` | no |
|  | `qae_open_report` | Path of the most recently saved report | no |
| AI agent testing | `qae_agent_suites` | Saved AI agent suites, the agent each tests, baseline status | no |
|  | `qae_agent_run` | Run a saved AI agent suite against the agent or another endpoint | yes |
|  | `qae_agent_run_status` | Progress, trust score, release gate and verdict of an agent run | no |
| Security and performance | `qae_security_scan` | Security headers, SSL/TLS and common vulnerability checks on a URL | yes |
|  | `qae_performance_test` | Load, stress, spike or soak test: latency percentiles, throughput, error rate | yes |
| Mobile | `qae_mobile_setup` | Device farm, app binary and handset configuration (links to the web app) | no |
| Account | `qae_status` | Connection, backend, key type, credits, requests this month, enabled services | no |
|  | `qae_connect` | Store an API key, or start browser sign-in | no |
|  | `qae_disconnect` | Forget the stored API key on this machine | no |

<!-- /qaeverest:tools -->

## Setup

1. Install the plugin from this repo's marketplace.
2. Give Claude Code your QAEverest API key:

   ```bash
   export QAEVEREST_API_KEY=qae_your_key_here
   ```

   Or run `/qaeverest:connect` and paste it once — it is stored in `~/.qaeverest/credentials.json` with mode `0600`, and never in the plugin.
3. `/qaeverest:usage` to check it works.

No API key yet? [Sign up free](https://qaeverest.ai/api-client/signup?source=claudecode) (no card), or get one from **Admin → API Management**.

**Requires Node 18+.** The server ships as a single bundled file (`dist/server.cjs`); there is nothing to `npm install`.

## How it differs from the IDE extensions

Two things an editor can do that a Claude Code tool call cannot, and what happens instead:

**Dialogs.** When a flow needs a value it doesn't have — a search query, a test type, a domain — the IDE opens an input box. Here the tool returns `needs_input` with the questions, Claude asks you in chat, and calls the tool again with your answers. The core's slot-filling logic is untouched; only who does the asking changes.

**Approvals.** When the copilot proposes something that costs credits or starts a real run, the IDE shows an approve/reject card. Here the tool returns `awaiting_approval`, Claude asks you, and `qae_approve` settles it. **Nothing the copilot proposes bills without that round trip** — and Claude is instructed not to answer on your behalf. The direct tools (`qae_generate_testcases` and the other `qae_generate_*` tools, `qae_security_scan`, `qae_performance_test`, `qae_agent_run`) are single calls with no copilot in between: Claude Code's own confirmation before it runs a tool is the approval, so don't auto-allow them if you want to see each one first.

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

- [`qaeverest-mcp`](https://www.npmjs.com/package/qaeverest-mcp) — the same MCP server on npm, for clients without a QAEverest plugin. It offers the slash commands above as MCP prompts.

## Privacy

See [PRIVACY.md](PRIVACY.md) for what is sent to the QAEverest backend and how it is handled.

## License

MIT — see [LICENSE](LICENSE).
