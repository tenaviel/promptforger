# Test cases

Manual checks for Promptforger. Run each raw input through the Skill and compare to the expectations. "Pass" needs all checks.

For every case, also confirm: the project is not built, the output follows the format (style line plus prompt in a code block), and no major feature, technology or integration appears that the user didn't imply.

| # | Raw input | Expected style | Must include | Must NOT include |
|---|---|---|---|---|
| 1 | `make todo app` | Compact | Add, complete and delete tasks; a short paragraph; open platform/stack | Accounts, database server, sync, tags, deployment |
| 2 | `discord bot tickets ban logs roles` | Thorough | Ticket flow, ban command, log channel, permissions, config and token handling; "roles" flagged as ambiguous | A specific hosting provider, web dashboard, economy or music features |
| 3 | `build fastapi api with sqlite auth` | Thorough | FastAPI and SQLite preserved; hashed passwords, token or session handling, validation, auth tests | Postgres, Docker, OAuth providers, rate-limit infrastructure |
| 4 | `unity car game endless road` | Thorough | Unity and C#; road segment recycling; car controls; camera; performance note | Multiplayer, shop, monetization, obstacles presented as requirements |
| 5 | `fabric mod that adds backpacks` | Thorough | Fabric kept; version stated or flagged; persistent contents; no nesting; multiplayer sync | A full client rewrite, extra mod features, other loaders |
| 6 | `add login to my website` | Thorough | Inspect existing project first; reuse conventions; no unnecessary rewrites; no assumed framework | A named framework or auth provider the user never mentioned |
| 7 | `quickly make python password generator` | Quick Build | Says first working version matters; minimal dependencies; `secrets` | GUI, packaging, test suite, CI |
| 8 | `build public SaaS dashboard with users` | Production-Ready | Authz per user, security, config/secrets, logging, tests, docs, deployment; dashboard purpose flagged as unknown; out-of-scope list | Billing, admin panel or analytics presented as requirements |
| 9 | A detailed, already-structured prompt (see below) | Compact or Thorough, matching its size | Original wording and structure largely intact; note lists what changed | Length growth beyond a few added lines |
| 10 | `make it look good` | Compact | Inspect first; use existing stack; don't change functionality | An invented design system, new framework, or redesign of the whole app |
| 11 | `make this production ready: simple cli that renames files` | Production-Ready (explicit) | CLI-appropriate hardening: validation, dry-run or safety, tests, docs, packaging | Kubernetes, databases, monitoring stacks |
| 12 | `tee discord-botti joka antaa roolit reaktioilla` | Compact | Prompt written in Finnish; reaction roles; permissions check | English output |
| 13 | `pforge: discord bot tickets ban logs roles` | Thorough | Same result as case 2: the shorthand prefix triggers Promptforger and the bot is not built | The bot's code |
| 14 | `promptforger: make todo app` | Compact | Same result as case 1 | The app's code |

## Case 9 input

> Write a Python CLI called `logtrim` that reads a log file path from argv, removes lines older than N days (--days, default 30) based on the ISO-8601 timestamp at the start of each line, and writes the result to stdout. Lines without a parsable timestamp are kept. Use only the standard library. Include pytest tests for the timestamp parsing and the boundary day. Output the full source in one file.

Expected: nearly unchanged, perhaps one added sentence (see `examples/compact.md`, example 5).

## Cross-style check

Run `make a python password generator` four times, asking for each style. The outputs should differ in priorities, not only length:

- Compact: a short paragraph with essential behavior.
- Thorough: character classes, validation, clipboard/UI considerations, error handling, tests.
- Quick Build: single file, standard library, "first working version" stated, no extras.
- Production-Ready: `secrets`, validation, package structure, tests, packaging, docs, release notes.
