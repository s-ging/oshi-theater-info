# 0009 — Performance budget

**Date:** 2026-10-29 (standing rules added 2026-11-02)
**Decided by:** Krischan
**Status:** accepted

## Context

Krischan: "if the look is the Nintendo DS settings, then it should run like it belongs in the DS without the slog. I want maximum performance gains on this, whatever means necessary," without trading away UX (2026-10-29). His standing rules for his projects (2026-11-02): ultrathin; the cheapest correct thing first, with a number on its cost; idle costs nothing; old hardware is the target.

## Decision

Accepted on 2026-10-29:

- No fixed render loop: redraw only on change; a short timer only while an animation plays.
- 256×192 per screen, whole-number scaling.
- No CSS 3D tilt.
- Avatars shrunk once to 16×16 with a small palette; the original is thrown away.
- Never touch YouTube's page layout.
- Binary protocol.
- Heartbeat under 30 seconds, answered by auto-response.

Details and the remaining proposals are in [product/architecture.md](../product/architecture.md#performance-budget).

## Replaces from the original handoff

- 480×270 internal resolution, a constant 12fps loop (6fps in background tabs), and RAM targets of the browser's total. These cost CPU while idle or measured the wrong thing.

## To do

Put numbers on every rule (bytes per message, wakeups per minute, cost per viewer-hour) once the protocol exists.
