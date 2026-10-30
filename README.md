# Promptforger

**Turn messy, half-formed ideas into prompts an AI (or a developer) can actually build from.**

Promptforger is a community-made, open-source [Claude Skill](https://docs.claude.com). It is not an official Anthropic product and is not affiliated with or endorsed by Anthropic.

You give it something like `discord bot tickets ban logs`. It gives back a clear, right-sized prompt. It does not build the project; it writes the prompt you'd hand to whoever (or whatever) will.

## The problem

Raw prompts are usually either too thin ("make website for game stats") or, once people try to fix that, bloated: invented databases, payment systems and cloud setups nobody asked for. Both waste time. Promptforger aims for the middle: understand what you meant, keep your intent, add only the detail that helps, and stop.

> **Raw:** `make python password generator with gui`
>
> **Promptforger (Compact):** Create a Python desktop password generator with a simple GUI. Allow users to choose password length and character types, generate secure random passwords, copy the result to the clipboard, and regenerate passwords without restarting the application. Keep the interface clean and easy to use.

> **Raw:** `add login to my website`
>
> **Promptforger (Thorough):** a prompt that first tells the implementer to inspect your existing stack and auth code, then asks for hashed passwords, safe sessions and protected routes, while forbidding unrelated rewrites. See [`examples/thorough.md`](examples/thorough.md).

## How it works

```text
raw idea → understood intent → style selection → implementation-ready prompt
```

1. **Understand.** What are you building? What type of project is it? Which technologies and requirements did you actually state?
2. **Sort details.** Stated or implied details become requirements. Small, harmless assumptions are made and kept visible. Big decisions you didn't make (hosting, database, payments) are left open or flagged, never invented.
3. **Pick a style** (below).
4. **Write the prompt**, structured for that style and project type.

## The four styles

| Style | Use for | Emphasis |
|---|---|---|
| **Compact** (default) | Small utilities, simple sites, clear requests | Goal, key requirements, tech, constraints. A short paragraph. |
| **Thorough** | Several interacting systems, multiple user flows, non-trivial logic | A project brief: features, flows, edge cases, error handling, testing, deliverables |
| **Quick Build** | Prototypes, MVPs, "just make it work" | A working first version: minimal dependencies and structure, no over-engineering, but no insecure shortcuts |
| **Production-Ready** | Public release, real users, commercial or security-sensitive software | Architecture, security, validation, logging, config, tests, docs, deployment, only as the project needs |

The styles differ in *priorities*, not just length. Compare the same password-generator idea across [`compact.md`](examples/compact.md), [`quick-build.md`](examples/quick-build.md) and [`production-ready.md`](examples/production-ready.md).

## Automatic style selection

You don't have to pick. Promptforger checks, in order:

1. **You named a style** ("make this compact", "production ready") → that style.
2. **Production signals:** public release, real users, commercial use, payments, public APIs, deployment, "production" → Production-Ready.
3. **Speed signals:** "prototype", "MVP", "quick", "just make", "proof of concept", "first version" → Quick Build.
4. **Complexity signals:** multiple systems or user flows, game logic, larger bots, risky ambiguity → Thorough.
5. **Otherwise** → Compact.

Judgment calls: login on its own doesn't make something Production-Ready (it gets Thorough with a security section); login plus public deployment does. If "quick" and "public SaaS" collide, the audience wins and the scope stays small.

## Output

```text
Selected style: Compact

[the finished prompt in a code block]

(optional one-to-three line note about assumptions or open decisions)
```

Ask for "just the prompt" and you get only the prompt.

## Install

Menu names change between releases; check Anthropic's current Skills documentation if something differs.

**Claude.ai**
1. Download this repository as a ZIP, so the archive contains a `promptforger/` folder with `SKILL.md` inside.
2. Open Settings → Capabilities (Skills section), enable Skills, and upload the ZIP.

**Claude Code**
Copy the folder into your skills directory:

```bash
# available in all projects
cp -r promptforger ~/.claude/skills/

# or only in one project
cp -r promptforger your-project/.claude/skills/
```

**Other** (API, other agents that read the Agent Skills format): the Skill is a plain `SKILL.md` plus Markdown examples with no scripts or dependencies, so follow your platform's instructions for adding a skill folder.

## Using it

Start a message with any of these prefixes, followed by your raw idea:

| Prefix | Example |
|---|---|
| `Use Promptforger on:` | `Use Promptforger on: make todo app` |
| `promptforger:` | `promptforger: make todo app` |
| `pforge:` | `pforge: make todo app` |

You can also ask in plain words:

- "Use Promptforger on: discord bot tickets ban logs roles"
- "Forge a prompt for: unity car game endless road"
- "Improve this prompt: make todo app"
- "pforge: make this production ready: build public SaaS dashboard with users"
- "Rewrite this prompt, only the prompt please: ..."

Promptforger is meant to trigger when you want a *prompt*. A plain "make me a todo app" should just build the app.

## Repository structure

```text
promptforger/
├── SKILL.md                    # The Skill: frontmatter + instructions
├── README.md                   # This file
├── LICENSE                     # MIT
├── examples/
│   ├── compact.md              # Utility, website, vague input, already-good prompt
│   ├── thorough.md             # Discord bot, Unity, Minecraft, existing-project feature
│   ├── quick-build.md          # Prototype-style requests
│   └── production-ready.md     # Public / commercial software
└── tests/
    └── test-cases.md           # Raw prompts with expected style and pass/fail checks
```

`SKILL.md` stays short on purpose: Claude loads it every time the Skill triggers. Longer material belongs in `examples/`, which Claude reads only when needed.

## Contributing

Good contributions are practical ones:

- Add a realistic raw prompt to `tests/test-cases.md` where the Skill picks the wrong style or invents features, and fix the instructions.
- Add an example for a project type or language not yet covered.
- Tighten wording in `SKILL.md`. Shorter and clearer beats longer.

Before opening a pull request, run your changes against the test cases and check: right style? User intent preserved? Nothing invented? Small requests still small? Please don't turn Promptforger into a general coding assistant, and avoid adding scripts or dependencies unless they clearly pay for themselves.

## License

MIT. See [LICENSE](LICENSE).
