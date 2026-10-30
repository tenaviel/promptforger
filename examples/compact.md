# Compact examples

Compact is the default: ordinary requests, small utilities, simple sites. A few sentences, no headings.

---

## 1. Simple Python utility

**Raw input**

> make python password generator with gui

**Selected style:** Compact

```text
Create a Python desktop password generator with a simple GUI. Allow users to choose password length and character types, generate secure random passwords, copy the result to the clipboard, and regenerate passwords without restarting the application. Keep the interface clean and easy to use.
```

Note: "secure random" is a reasonable assumption for a password tool. No tests, packaging or settings screen were added.

---

## 2. Website

**Raw input**

> make website for game stats with login and dark theme

**Selected style:** Compact

```text
Build a website that displays game statistics, with user login and a dark theme. Present stats in readable tables or simple charts, and make the pages work on desktop and mobile. Users should be able to sign up, log in and log out, and pages that need login should be protected. The game, the stats source and what logged-in users get beyond viewing are not specified, so use sample data behind a clear, swappable interface and list any assumptions you make. The technology stack is open: pick a straightforward one and state your choice.
```

Note: Login was requested, so it stays. No OAuth, payment, admin panel or specific database was invented.

---

## 3. Caveman prompt

**Raw input**

> python thing that gets weather and saves it

**Selected style:** Compact

```text
Write a Python script that fetches the current weather for a location and saves it to a file. Take the location as a command-line argument. Use a free weather API that needs minimal setup, say which one you chose and how to get any required key, and read the key from an environment variable rather than the source code. Append each result with a timestamp to a local file (CSV or JSON Lines), show a clear message on network errors or an unknown location, and include a short usage example. Done when running the script once adds a correctly formatted entry to the file.
```

Note: The API and file format were left to the implementer on purpose.

---

## 4. Extremely vague prompt

**Raw input**

> make it look good

**Selected style:** Compact

```text
Improve the visual design of this project. First inspect it to identify what it is (website, app, UI, etc.), how it is currently styled, and which parts look weakest. Then make focused improvements to layout, spacing, typography, color and consistency using the project's existing stack and styling conventions. Do not change functionality or restructure the code. If it's unclear which page or screen is meant, work on the main user-facing view and tell me which one you chose. Finish with a short summary of what changed.
```

Note: With no project details, the prompt tells the implementer to look first instead of inventing a design direction.

---

## 5. Already-good prompt (kept, not inflated)

**Raw input**

> Write a Python CLI called `logtrim` that reads a log file path from argv, removes lines older than N days (--days, default 30) based on the ISO-8601 timestamp at the start of each line, and writes the result to stdout. Lines without a parsable timestamp are kept. Use only the standard library. Include pytest tests for the timestamp parsing and the boundary day. Output the full source in one file.

**Selected style:** Compact

```text
Write a Python CLI called `logtrim` that reads a log file path from argv, removes lines older than N days (--days, default 30) based on the ISO-8601 timestamp at the start of each line, and writes the result to stdout. Lines without a parsable timestamp are kept. Exit with a non-zero status and a clear message if the file can't be read. Use only the standard library. Include pytest tests for the timestamp parsing and the boundary day. Output the full source in one file.
```

Note: One sentence added (unreadable-file behavior). Everything else is untouched.
