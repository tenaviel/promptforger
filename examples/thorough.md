# Thorough examples

Thorough fits multiple interacting systems, several user flows, non-trivial logic, or ambiguity that would cause rework. Think "well-written project brief", not padding.

---

## 1. Discord bot

**Raw input**

> discord bot tickets ban logs roles

**Selected style:** Thorough

```text
Build a Discord bot with a support ticket system, moderation commands, action logging and role management.

Language and library are not specified: use a mainstream, actively maintained Discord library (e.g. discord.py or discord.js) and state your choice.

Core features
- Tickets: a member opens a ticket via a slash command or button. The bot creates a private channel visible only to that member and staff. Staff can close the ticket, which archives or deletes the channel.
- Moderation: ban and unban commands with an optional reason. Only configured staff roles may use them. The bot must refuse to act on users it cannot moderate (higher role, owner, itself).
- Logging: post an embed to a configurable log channel for ticket open/close and every moderation action (actor, target, reason, time).
- Roles: use roles for permissions (which roles count as staff, configurable), and provide a command for authorized staff to add or remove a role from a member. If a different role feature was intended (self-assign, reaction roles), ask before building it.

Technical requirements
- Request only the gateway intents the features need.
- Read the bot token from an environment variable. Keep channel and role IDs in a config file. Provide an example config with no secrets.
- Persist open-ticket state so tickets survive a restart. Use simple storage appropriate to the scale and say what you chose.

Error handling
- Handle missing permissions (user and bot), unknown users, and users with DMs closed. Reply with clear ephemeral error messages.

Testing
- Provide a manual test checklist for a throwaway test server. Add unit tests for the permission-check logic if practical.

Deliverables
- Source code, example config, and a README covering setup (creating the application, invite permissions) and the command list.

Done when a staff member can run this flow in a test server: open a ticket, close it, ban a user, assign a role, see every step in the log channel, and restart the bot without losing open tickets.
```

Note: "roles" is ambiguous, so the prompt covers the safe reading and tells the implementer to ask about the others.

---

## 2. Unity game

**Raw input**

> unity car game endless road

**Selected style:** Thorough

```text
Build an endless-road car game in Unity (C#). The player drives a car along a road that generates indefinitely.

Core gameplay
- The player steers the car; the car moves forward at a speed that increases gradually.
- The road is built from segments generated ahead of the car and recycled behind it (object pooling), so the game can run indefinitely without growing memory use or hitching.
- A camera follows the car.

Assumptions (adjust if wrong)
- Keyboard controls on PC using Unity's current Input System.
- Distance traveled is shown as a score on a simple HUD, with a restart option. Obstacles, traffic and a fail state were not requested; structure the code so they can be added later, but don't build them.
- Choose 2D or 3D, state which, and keep art to simple placeholder primitives or free assets.
- Use the current Unity LTS version and state it.

Technical requirements
- Organize into scenes, prefabs and small single-purpose scripts (car controller, road generator, HUD). Explain the setup of each prefab and scene so the project opens and runs without manual wiring.
- Keep frame rate stable on a mid-range PC; avoid per-frame allocations in the road generator.

Testing
- Describe how to verify: drive for several minutes, confirm no visible seams, gaps or memory growth, and confirm restart resets all state.

Deliverables
- The Unity project files or the scripts and setup steps needed to recreate it, plus a short README with controls and how to run.

Done when the car can drive indefinitely on a seamless road with a visible score and a working restart.
```

Note: Obstacles and traffic were deliberately left out because the user didn't ask for them.

---

## 3. Minecraft mod

**Raw input**

> fabric mod that adds backpacks

**Selected style:** Thorough

```text
Create a Fabric mod for Minecraft (Java) that adds backpacks: items that give the player extra inventory space.

Minecraft version is not specified: target the latest stable version supported by Fabric and state it.

Core features
- A backpack item that opens a storage GUI when used (right-click). Start with one backpack type and a fixed slot count (e.g. 27) kept in one easily changed constant.
- Contents are stored with the item itself, so they persist when the backpack is dropped, moved between inventories, or the player relogs.
- A crafting recipe and a placeholder texture and model.
- Wearing the backpack visibly on the player is not requested; do not implement it.

Edge cases
- A backpack must not be placeable inside itself or any other backpack (prevents loops and item duplication).
- Handle the backpack being moved or dropped while its GUI is open.

Technical requirements
- Handle the screen/container logic correctly for multiplayer: inventory changes are validated on the server and stay in sync with the client.
- Use the standard Fabric project template and Fabric API. Provide a valid fabric.mod.json.

Testing
- Provide a manual checklist for a dev client and a dedicated server: open, store, drop, pick up, relog, die with the backpack, try nesting.

Deliverables
- A buildable Gradle project and a README with build and install instructions.

Done when the backpack can be crafted, filled, dropped, picked up and reopened with contents intact, in both singleplayer and on a server.
```

---

## 4. Existing-project feature request

**Raw input**

> add login to my website

**Selected style:** Thorough (existing code plus security-sensitive feature)

```text
Add user login to my existing website.

Before changing anything, inspect the project: its stack, routing, how pages and any backend are structured, whether user, session or auth code or a database already exists, and its UI conventions. Give me a short summary of what you found and your plan, then implement.

Requirements
- Login and logout. Registration was not specified: if there is no other way for accounts to be created, add simple sign-up; otherwise reuse what exists.
- If the project has no user storage, add the simplest persistent option that fits the existing stack. If it has one, reuse it.
- Hash passwords with a standard, well-reviewed algorithm. Never store or log plaintext passwords.
- Use session or token handling appropriate to the stack, with secure cookie settings and CSRF protection where applicable.
- Which pages require login was not specified: make protection easy to apply per route, apply it only to clearly user-specific pages, and tell me which you chose.
- Show a generic message on failed login (don't reveal whether the username exists).

Constraints
- Don't rewrite unrelated code or change the existing design language. Match current styling for the new forms.
- Don't add third-party identity providers unless the project already uses one.
- Keep secrets in environment variables, not in source.

Testing
- Verify successful login, failed login, logout, and that a protected route redirects when logged out. Run the project's existing tests if any.

Finish with a summary of changed files and any configuration I need to set.
```

Note: The prompt never assumes a framework; it tells the implementer to detect it.
