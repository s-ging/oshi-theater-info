# How we work

Our working principles, written down so every session and agent works the same way. [AGENTS.md](AGENTS.md) holds the short, binding version; this file explains them.

## Two modes

Not every conversation needs the full rulebook. Pick the mode from what the session is about to touch.

### Brainstorm mode (the default for conversation)

For talking ideas through, research, analysis, mockups, and writing inside this repository.

- **Start immediately.** No restating, no three questions, no waiting for a yes. Ask questions alongside the first results, not before them.
- Pareto still applies: lead with what matters most.
- Nothing outside this repository changes in this mode.

### Work mode (trial by fire)

For anything that touches **code**, a **deploy**, an **account** (Cloudflare, domain, GitHub settings, payment platforms), a **public post**, or anything **hard to undo**.

- Run the [confirmation gate](AGENTS.md#confirmation-gate): restate the ask, say what you understood and what is out of scope, ask **at least three** clarifying questions (which repo, which environment, what "done" means, what must stay as it is), and wait for an explicit yes before writing code.
- Chesterton's fence is front and center.
- Pareto decides the order of the work.

### Switching

- Moving from brainstorm to work mode happens the moment a session is about to change code or anything outside this repository. Say so in one line ("This touches the code, so switching to work mode") and run the gate.
- The person you are working with can also switch explicitly: "work mode" or "brainstorm mode".
- When unsure which mode applies, it is work mode.

## Chesterton's fence

Do not remove, rename, or clean something up until you know why it is there.

That includes code, config, copy, a branch, and a step in a process. If you cannot say what it is for, leave it. Find out first in [decisions/](decisions/) and [logs/](logs/), then ask a teammate.

This product already has dropped ideas (curved seating, a silhouette row on the video, reading YouTube cookies). They are recorded with their reasons so nobody brings them back without knowing why they went.

## Pareto principle

Start with the small part of the work that carries most of the result. About 20% of the effort usually drives about 80% of the outcome. When that path is clear, do it first.

For this product the high-leverage question is simple: does a group of friends keep the window open for a whole stream? Build toward answering that before anything else.

## Performance

Krischan's standing rules for his projects (stated 2026-11-02):

- **Ultrathin.** Absolute mastery of optimization; the minimal approach; push the limits.
- **Put a number on it.** Design the cheapest correct thing first and state its cost: per message, per second, per viewer, per month. "Cheap enough" is not an answer.
- **Lazy over live.** Idle costs nothing: no polling, no timers or loops running when nobody acts.
- **Old hardware is the target.** Old PCs and old Android and iOS devices, so literally everyone can join.

For this product that means "runs like it belongs on a DS, without the slog," and never trading away UX to get there. The concrete budget is in [decision 0009](decisions/0009-performance-budget.md) and [product/architecture.md](product/architecture.md).

## Jakob's law

People spend most of their time in other apps, so ours should work the way they expect. The DS look is the costume; the controls underneath behave like normal web controls, with words on buttons and the main action where people look for it. See [decision 0003](decisions/0003-design-for-familiarity.md).

## Copy

Write like a person talking to a friend in the fandom. Never use generic AI-sounding copy: no grand label-plus-tagline pairs ("Home — Your window to the world"), no "all in one place", "on your time", "you control who sees…", or "one-of-a-kind personalized feed". Krischan calls this pattern aggressive and stupid. More in [product/brand.md](product/brand.md#copy).

---

Authored by Krischan.
