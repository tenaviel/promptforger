# Quick Build examples

Quick Build is for prototypes, MVPs and "just make it work" requests. The prompt says outright that a working first version beats architecture, while still refusing insecure or broken shortcuts.

---

## 1. Password generator, quick version

**Raw input**

> quickly make python password generator

**Selected style:** Quick Build ("quickly")

```text
Write a single-file Python script, password_gen.py, that generates a random password and prints it. The priority is a working first version that is easy to run and tweak, not production architecture. Use only the standard library and generate passwords with the `secrets` module, not `random`. Accept an optional --length argument (default 16) and include letters, digits and symbols. A command-line tool is fine for this first version. No tests or packaging needed. Done when `python password_gen.py` prints a password immediately and `--length 24` prints a longer one.
```

Note: Speed trimmed the scope (no GUI, tests, packaging). It did not trim secure randomness.

---

## 2. Prototype

**Raw input**

> prototype of a gym workout tracker, just need something working to test the idea

**Selected style:** Quick Build ("prototype", "just need something working")

```text
Build a quick prototype of a workout tracker so I can test the idea. The priority is a working first version that is easy to run and modify. Keep dependencies and structure to a minimum.

Features: add a workout entry (exercise, sets, reps, weight, date), see a list of past entries newest first, and delete an entry. Nothing else: no accounts, sync, charts or settings.

Platform wasn't specified. Unless you have a simpler idea, make it a single-page web app (one HTML file with inline CSS and JavaScript, no build step) that stores entries in the browser's local storage. Keep the UI plain but usable on a phone screen.

Done when I can open the file, add entries, reload the page, and still see them.
```

Note: The platform is offered as a suggestion, not stated as a user requirement.
