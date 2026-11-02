# 0001 — A Git knowledge base as the single source of truth

**Date:** 2026-11-03
**Decided by:** Krischan
**Status:** accepted

## Context

The product so far lives in chats, mockups and an earlier handoff document from another AI. Chat history does not carry over between sessions, tools or models.

## Decision

Keep everything we know and decide about the product in `s-ging/oshi-theater-info` as Markdown, set up the same way as the team's other knowledge bases (from the `work-week/client-template` structure). `AGENTS.md` holds the rules and map; `CLAUDE.md` loads it for Claude Code. Every session that changes something leaves a log.

Adapted from the client template because this is the team's own product, not a client:

- `client/` became `product/` (overview, experience, architecture, brand, market, monetization, safety).
- No `deliverables/` folder and no `next-meeting.md`; there is no client to hand things to. Add them back if a partner or sponsor appears.
- No client approver. Krischan approves.

## Why

A new chat or agent reads the repo and is up to speed. Git history shows what changed, when and why.

## Alternatives considered

- Chat history or project memory in one AI tool: does not carry over between tools, models or teammates.
- Keeping code and knowledge in one repository: the team keeps tools and code out of knowledge bases.
