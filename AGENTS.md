# Oshi theater knowledge base

This repository is the single source of truth for the oshi theater: a small two-screen window, styled after the Nintendo DS settings screen, where VTuber fans sit beside their friends while they watch their oshi's livestream. Every AI agent (Claude Code or any other) and every teammate reads this file first.

"Oshi theater" is the working name of this repository, not the product name. The product has no name yet ([open questions](project/open-questions.md)). Until it does, write "[app name]" in any product copy.

If you are a new session: read this file, then [README.md](README.md), then [project/status.md](project/status.md). That is enough to be up to speed. Go deeper through the [map](#where-to-look) only as the task needs.

**Sync both ways.** Other sessions, agents and teammates edit this repository too. At the start of every session, pull the latest version (`git pull`) before reading or writing. At the end of any session that changed something, commit and push, so the next session sees it. Work that stays in a chat and never reaches this repository is lost.

## Absolute law

Do not break these rules. If anything elsewhere in this repository disagrees with this section, this section wins. If unsure, stop and ask, and do not take the looser reading.

### Who you are working with

The team sometimes shares accounts, so the account name, email or git config does not tell you who is at the keyboard. Before you author anything (a log, a decision, a commit, an "Authored by" line, an approval), ask who you are working with, unless they have already said so in this session. Use the name they give. Never guess it.

### Confirmation gate

Before changing anything outside this repository (the code repository, a deploy, the Cloudflare account, a domain, a store listing, a public post):

1. Restate the request in your own words: outcome, scope, constraints.
2. Say what you believe is out of scope.
3. Ask clarifying questions about anything vague.
4. Wait for explicit approval.

A restatement, silence, or an earlier conversation is not approval for a new change. Read-only work (reading, researching, drafting inside this repo) does not need the gate.

### Two modes

How strictly these rules apply depends on what the session touches. Full explanation in [PRINCIPLES.md](PRINCIPLES.md).

- **Brainstorm mode** (conversation, research, drafting inside this repo): start immediately; ask questions alongside the work, not before it.
- **Work mode** (code, deploys, accounts, anything hard to undo): run the confirmation gate with **at least three** clarifying questions and wait for an explicit yes before writing code. Chesterton's fence front and center.
- Switch to work mode the moment a session is about to change code or anything outside this repo, and say so. The person you are working with can switch explicitly ("work mode", "brainstorm mode"). When unsure, it is work mode.

### Chesterton's fence

Do not remove, rename, or clean something up until you know why it is there. If you cannot say what it is for, leave it. Find out first ([decisions/](decisions/), [logs/](logs/)). Then ask before you change it.

### Pareto principle

Start with the small part of the work that carries most of the result. When that high-leverage path is clear, do it first. No low-impact busywork while the useful path is still open.

### Performance is the craft

Design the cheapest correct thing first and put a number on its cost. Idle costs nothing: no polling, no running loops or timers when nobody acts. Old phones and old PCs are the target, not the edge case. Details in [PRINCIPLES.md](PRINCIPLES.md#performance) and [decision 0009](decisions/0009-performance-budget.md).

### No AI-generated art

No AI-generated graphics, sprites, avatars, emoji, icons or illustrations ship in the product or its marketing. VTuber fandoms reject AI art outright, and Krischan does not use it for anyone. Placeholder sprites in the early mockups were generated in code by an AI and must be replaced by human-drawn art before anything is public. See [decision 0004](decisions/0004-no-ai-art.md).

### Fans first

- Never charge for the social core: sitting together, party size, waving, presence.
- No ads. No selling or sharing user data. No gacha or loot boxes.
- Never sell anything based on a specific VTuber's likeness or marks.

See [product/monetization.md](product/monetization.md) and [decision 0008](decisions/0008-money-from-fans.md).

### Assume minors are in the room

VTuber fandoms include many teenagers. Strangers stay anonymous by default, links are shared only on mutual consent and only to known platforms, and no feature lets a stranger message someone directly inside the app. See [product/safety.md](product/safety.md).

### Credentials

Do not write passwords, API keys, tokens, recovery codes, or card or bank details into this repository in plain text. Record **which** accounts exist and **where** each login is kept in [map/accounts.md](map/accounts.md). See [decision 0002](decisions/0002-credentials.md).

### Other work

This repository is about the oshi theater only. Never bring in names, accounts or details from the team's clients or other repositories.

## Keeping this repository true

- **Facts carry a source and date.** Write where a fact came from (Krischan said it, a vendor's pricing page, a test) and when. Mark guesses and estimates as such. Prices and limits change: re-check before relying on them.
- **Stated vs proposed.** Mark what Krischan decided apart from what an agent proposed and nobody confirmed yet.
- **Research** goes in [research/](research/), one dated file per piece of work. Use the `research-note` skill.
- **The product** (what it is, how it behaves, how it is built, how it makes money) lives in [product/](product/). Update it when a decision changes it.
- **Our work** (status, scope, roadmap) lives in [project/](project/). Keep [project/status.md](project/status.md) current: it is the first thing a new session reads.
- **Decisions** that someone might later want to undo go in [decisions/](decisions/), including ideas that were tried and dropped, so nobody brings them back by accident.
- **Logs:** end every session that changed something with a log in [logs/](logs/). Use the `session-log` skill. Never rewrite an old log.
- **Open questions** go in [project/open-questions.md](project/open-questions.md), and come out when answered.
- Keep this file short. Put detail in linked files.

## Where to look

| Looking for | Go to |
| --- | --- |
| Where things stand right now | [project/status.md](project/status.md) |
| How we work: modes and principles | [PRINCIPLES.md](PRINCIPLES.md) |
| What the product is and who it is for | [product/overview.md](product/overview.md) |
| How the window looks and behaves | [product/experience.md](product/experience.md) |
| How it is built, performance budget, costs | [product/architecture.md](product/architecture.md) |
| Look, fonts, colors, copy rules, naming | [product/brand.md](product/brand.md) |
| Fandom culture, audience, launch market | [product/market.md](product/market.md) |
| How it makes money, transparency | [product/monetization.md](product/monetization.md) |
| Protecting users, especially minors | [product/safety.md](product/safety.md) |
| The first launch (v0) | [project/scope.md](project/scope.md) |
| The long-term plan | [project/roadmap.md](project/roadmap.md) |
| Questions waiting on a decision | [project/open-questions.md](project/open-questions.md) |
| Accounts, mockups, tools, where logins are kept | [map/accounts.md](map/accounts.md) |
| Research and sources | [research/](research/) |
| Why things are the way they are | [decisions/](decisions/) |
| What already happened | [logs/](logs/) |
