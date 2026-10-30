# Production-Ready examples

Production-Ready is for public, commercial or long-lived software. It adds engineering only where the project benefits, and says what is deliberately left out.

---

## 1. Password generator, published package

**Raw input**

> make a python password generator, production quality, I want to publish it on PyPI

**Selected style:** Production-Ready (explicit request plus public distribution)

```text
Build a Python password generator as a maintainable, publishable package with a command-line interface.

Behavior
- Generate passwords with the `secrets` module. Options: length, and which character classes to include (lowercase, uppercase, digits, symbols), plus an option to exclude ambiguous characters.
- Guarantee at least one character from each selected class.
- Never log, persist or echo generated passwords anywhere except stdout (or the clipboard, only if requested by a flag).

Validation and errors
- Reject invalid input (length below a sensible minimum, no character class selected) with a clear message and a non-zero exit code.

Structure
- Use a `src/` layout. Keep the generation logic in a pure, importable function separate from the CLI so it can be used as a library.
- Support currently maintained Python versions and state the minimum.

Testing
- Use pytest to cover length, class guarantees, ambiguous-character exclusion, input validation and CLI exit codes. Don't test randomness statistically beyond sanity checks.

Packaging and release
- Provide pyproject.toml with a console-script entry point, a license, and version metadata. Add a simple CI workflow that runs tests and a linter.

Documentation
- README with install, CLI usage, library usage and a short security note explaining the randomness source.

Done when `pip install .` provides a working command, all tests pass, and the package builds cleanly for upload to PyPI.
```

---

## 2. Public SaaS dashboard

**Raw input**

> build public SaaS dashboard with users

**Selected style:** Production-Ready ("public", "SaaS", user accounts)

```text
Build a public, multi-user SaaS dashboard web application intended for real users.

What the dashboard shows and where its data comes from are not specified. Build the platform foundation below first. If the purpose and data sources aren't provided elsewhere, ask me before implementing dashboard content beyond one clearly labeled example view.

Accounts and access
- Sign up, log in, log out and password reset.
- Every user sees only their own data. Enforce authorization on the server for every data access, not just in the UI.
- One user role unless I specify otherwise.

Security
- Hash passwords with a modern algorithm. Use secure session handling (HTTPS-only, HttpOnly, SameSite cookies) and CSRF/XSS protection.
- Validate and sanitize all input server-side. Rate-limit authentication endpoints.
- Keep secrets in environment variables, with separate dev and production configuration. Include dependency vulnerability scanning in CI.

Architecture and data
- Stack is not specified: choose a mainstream, well-supported one and justify it briefly.
- Persistent database with schema migrations. Document the backup approach.
- Keep the data layer behind an interface so the dashboard's data sources can be added later.

Reliability and operations
- Structured logging that never records passwords or tokens, a health-check endpoint, and error reporting hooks.
- Containerized or platform-agnostic deployment instructions.

Quality
- Unit and integration tests for authentication and authorization, plus an end-to-end smoke test (sign up, log in, view dashboard, log out). CI runs all tests on every change.
- Responsive layout and baseline accessibility (keyboard navigation, labels, contrast).

Not requested, so do not build now: billing or payments, admin panel, analytics, team or organization features. Don't block them architecturally.

Deliverables
- Source code, migrations, CI configuration, README with local setup, an environment-variable reference, and deployment steps.

Done when a new user can register, log in, see only their own dashboard, and the app deploys from the documentation with all tests passing.
```

Note: Payments, admin panel and analytics are named as out of scope instead of being invented.
