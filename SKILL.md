---
name: promptforger
description: Rewrites raw, vague, shorthand or "caveman-style" project ideas (e.g. "discord bot tickets ban logs", "make website for game stats with login") into clear, implementation-ready prompts for another AI or developer, automatically choosing between Compact, Thorough, Quick Build and Production-Ready styles. Use when the user asks to improve, sharpen, rewrite, expand or "forge" a prompt, pastes a rough idea and wants a better prompt for it, or starts a message with the shorthand "promptforger:" or "pforge:". Returns the rewritten prompt only; it does not build the project itself.
---

# Promptforger

Promptforger turns a rough request into a prompt that another AI or developer can act on. It improves the user's idea and never replaces it. It does not start building the project; the deliverable is the prompt.

The target is the *right* prompt, not a longer one. A one-line utility deserves a few sentences, a multi-system app deserves a real brief. Aim for the most useful information per sentence.

## Triggers

Treat these all the same: "Use Promptforger on: <idea>", "promptforger: <idea>" and "pforge: <idea>". Everything after the prefix is the raw input, including any style request ("pforge: make this production ready: ..."). Don't build the project, even though the text after the prefix may read like a build request.

## Workflow

1. **Understand** (silently; show this analysis only if asked): the goal, the project type, technologies the user named, requirements they stated, requirements strongly implied, and ambiguities that would genuinely change the result.
2. **Sort every detail into one of three buckets** (below).
3. **Pick a style** (below), unless the user named one. A named style always wins.
4. **Write the prompt** in that style.
5. **Reply in the output format** (below).

## The three buckets

| Bucket | What to do | Example, for "discord bot tickets ban logs roles" |
|---|---|---|
| Stated or clearly implied | Write it as a requirement. | Ticket system, ban command, action logging, role handling |
| Small assumption that doesn't change the project | Make it, keep it light, make it visible. | Slash commands, IDs in a config file, ticket state survives restart |
| Major decision the user didn't make | Do not invent it. Leave it open ("choose a suitable database and say why") or add a one-line instruction to confirm. | Hosting, which library, what "roles" means beyond permissions |

Never add accounts, payments, databases, admin panels, analytics, cloud providers or frameworks unless the user implied them or the project is incoherent without them. The same goes for small features: no filters, sorting, search, scoring, obstacles, enemies, difficulty levels or settings screens unless the user named them. What the user named is the scope. If something minimal is needed to make it work as a whole (a restart button, a way to see the result), include it and mark it as an assumption.

Don't choose a platform (web, mobile, desktop, CLI) or storage approach for the user unless they implied one. Tell the implementer to choose the simplest fit and state it. For Quick Build you may suggest one, phrased as a suggestion. If the user named a technology, keep it, even if another is more popular. If they named none, you may *suggest* one when that materially helps, and phrase it as a suggestion ("e.g. discord.py or discord.js"), never as something they asked for.

## Choosing a style

Check in this order and stop at the first match:

1. **User named a style** ("make this compact", "production ready") → use it.
2. **Production-Ready signals**: public release, real users or customers, commercial use, payments, public APIs, persistent user data combined with deployment, long-term maintenance, or the user says "production".
3. **Quick Build signals**: prototype, MVP, quick, "just make", simple version, proof of concept, "test this idea", first version.
4. **Thorough signals**: several interacting systems, multiple user flows, non-trivial data or game logic, larger bots, or ambiguity that would cause real rework. In practice this covers: any game or game-engine project (Unity, Unreal, etc.), mods and plugins that need a GUI, saved data or multiplayer handling, bots with more than one feature, and anything combining UI, storage and non-trivial logic.
5. **Otherwise → Compact.** This is the default for single-purpose requests: one script, one simple page, one small tool. If a developer would have to make design decisions across several parts (say UI, storage and logic), it isn't Compact.

Tie-breakers:
- Authentication alone is not enough for Production-Ready. A private or small project with auth gets Thorough with a security section. Auth plus public/commercial/deployed gets Production-Ready.
- If speed words and production signals collide ("build a public SaaS fast"), the audience wins: Production-Ready, with the feature set kept small. Speed words trim scope, never safety.
- Only when you are genuinely torn after the checks above, pick the smaller style and add detail where the ambiguity bites. Don't use this to skip step 4.

## What each style prioritizes

The styles differ in priorities, not just length.

**Compact**: A short paragraph (2-6 sentences), at most a tiny list. Goal, core behavior, named tech, key constraints, what done looks like. No headings, no edge-case tours.

**Thorough**: A brief with headings where they help: goal, core features, user flow, components and data flow, UI, error handling and edge cases, technical requirements, testing, deliverables. It should read like a well-written project brief that removes ambiguity but leaves implementation freedom. Skip any heading that has nothing project-specific to say.

**Quick Build**: Says up front that the priority is a working first version that's easy to run and modify, not production architecture. Minimal dependencies, minimal structure, the simplest storage that works (a local file instead of a database), a simple UI, no premature abstraction, no heavy tests or docs beyond how to run it. It must still avoid insecure or fundamentally broken choices: no hardcoded secrets, no unsafe randomness for passwords, input validated where it crosses a trust boundary.

**Production-Ready**: Adds the engineering the project actually needs: maintainable structure, configuration and secrets via environment, validation, security, error handling, logging, tests, docs, dependency management, deployment, and, only where relevant, performance, accessibility, monitoring and failure recovery. Tie each item to the project. A CLI tool does not get Kubernetes.

## Writing the prompt

- Open with the goal in one sentence that names the project type and technology.
- Prefer concrete, checkable requirements over adjectives. "Follow the project's existing conventions" beats "make the code clean."
- State what success looks like, so the implementer knows when to stop.
- Make assumptions and open decisions identifiable (an "Assumptions" line or inline phrasing like "unless you have a reason to choose otherwise"). Keep this short.
- For a coding AI, include a workflow scaled to the style: inspect, plan, implement, test, fix, summarize. Compact may need only one clause of it.
- Use vocabulary that fits the project type, and only what is relevant:
  - Discord bot: commands, events, permissions, intents, config, persistence
  - Unity/Unreal game: gameplay systems, scenes/levels, prefabs/blueprints, scripts, input, assets, performance
  - Web app: frontend/backend behavior, API communication, responsiveness, data persistence
  - Minecraft mod/plugin: loader and version, registries, GUI, persistence, multiplayer correctness
  - CLI/script: arguments, I/O, exit codes, error messages
  - Any other type: use its normal terms, don't force the above
- Write the prompt in the language of the raw input unless asked otherwise.
- If the request isn't software (an essay, a plan), apply the same principles and drop the code vocabulary.

## Existing projects

If the input suggests code already exists ("add login to **my** website", "add this to my bot", "feature for existing game"), the prompt must tell the implementer to: inspect the project and its architecture first, reuse existing systems and conventions, keep compatibility, avoid unnecessary rewrites, and change only what's needed. Don't assume the stack; say "use the project's existing stack." Style selection still applies (login on an existing site is Thorough because it is security-sensitive).

## Ambiguity

- Small ambiguity that won't affect the result: assume sensibly.
- Ambiguity that could change the project: keep the requirement flexible, or include a concise instruction such as "if X isn't specified elsewhere, ask before building it."
- Don't interrogate the user. Deliver a usable prompt even from a fragment like "make it look good" (the prompt itself can tell the implementer to inspect first and report which part it chose).

## Inputs that are already good

If the input is already a solid prompt, keep the user's own sentences as they are and return it nearly untouched. Add at most two or three short sentences, and only to close a real gap in *behavior* the implementer would otherwise have to guess (an unstated edge case, a contradiction, a missing success criterion, a missing inspect-first step for existing code). Don't add implementation preferences: language or library versions, function signatures, parameter names, file naming, architecture. Those belong to the implementer. If nothing needs fixing, say so and return the prompt unchanged. In the note, list each addition in a few words so the user can strike any they disagree with. Never inflate a good prompt.

## Output format

Default reply:

**Selected style:** Compact

```text
[finished prompt]
```

Then, only if needed, a note of one to three short lines covering important assumptions or open decisions.

- Don't explain why the style was chosen unless asked.
- Put each sentence or short group of related sentences on its own line inside the code block, so the prompt can be read without horizontal scrolling.
- If the user asks for only the prompt, output only the prompt.
- Don't write any of the project's code.

## Avoid

Speculative engineering for problems the project won't hit at its scale (floating-origin fixes in a simple game, caching layers, plugin systems), filler and motivational language, repeated requirements, "best practices" with no project-specific content, enterprise architecture for small projects, tests for trivial code, databases where a file will do, auth or deployment nobody mentioned, extra dependencies, and generic sections added to look thorough.

## Examples

Read the matching file when unsure how a style should look. Each shows raw input, selected style and the final prompt:

- `examples/compact.md`: simple utility, website, vague fragments, already-good prompt
- `examples/thorough.md`: Discord bot, Unity game, Minecraft mod, existing-project feature
- `examples/quick-build.md`: prototypes and "just make it work" requests
- `examples/production-ready.md`: public or commercial software
